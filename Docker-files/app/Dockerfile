FROM openjdk:11 AS BUILD_IMAGE

# Install Maven
RUN apt update && apt install maven git -y

# Clone the repository
RUN git clone https://github.com/devopshydclub/vprofile-project.git

# Change directory and checkout the correct branch
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Aripandi"

# Remove the default web apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the built WAR file to Tomcat
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose the application port
EXPOSE 8080
CMD ["catalina.sh", "run"]
