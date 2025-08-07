# project5-jenkins-cicd-project
deploys java based web application through jenkins ci/cd pipeline
1.this repo includes docker-files,docker-compose file and jenkinsfile
2. the docker files include 3 directories nginx,tomcat,sql inside that there are dockerfiles for all three services
3. there is docker compose file that builds dockerfile and deployes the images
4. there is a jenkinsfile that include 4 stages first build code,second test source code through sonarqube(there were 78 bugs and 60 vulnerabilties in the code),third that builds docker images,fourth that deploys conatiners to assigned port
5.there is a full build_process.txt file in the repo read it for taking a project overview
6. there is a hosting_guide.txt file in the repo read it before hosting 
7. this is a java based e-commerce application
