FROM maven:3.9.9 AS build_image
RUN git clone https://github.com/yashdua12/project5-jenkins-cicd-project.git
WORKDIR /project5-jenkins-cicd-project
RUN mvn install 

FROM tomcat:10-jdk21-openjdk
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build_image project5-jenkins-cicd-project/target/beauty-store.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"] 
