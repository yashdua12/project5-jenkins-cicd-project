pipeline {
    agent any
     tools {
        maven "maven"
        jdk "java21"
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
