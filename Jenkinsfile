pipeline {
    agent any
     tools {
        maven "maven"
        jdk "java21"
    }
    environment {
        scannerHome = tool 'Sonar1'  
        DOCKER_HOST = "" // NAME OF DOCKER you have placed in system of jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/yashdua22/jenkins-ci-cd-project-.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving it...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

         stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarserver') { 
                    sh """
                        sonar-scanner \
                        -Dsonar.projectKey=jenkins-ci-cd-project- \
                        -Dsonar.projectName=mizo-beauty \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.sources=src/ \
                        -Dsonar.java.binaries=target/classes/ \
                        -Dsonar.junit.reportsPath=target/surefire-reports/ \
                        -Dsonar.jacoco.reportPaths=target/jacoco.exec \
                        -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml
                    """
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('jenkins-ci-cd-project-') {
                    sh 'docker compose build'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                dir('jenkins-ci-cd-project-') {
                    sh 'docker compose up -d'
                }
            }
        }
    }
}
