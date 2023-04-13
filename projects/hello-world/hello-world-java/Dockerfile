# Build a JAR File
FROM maven:3.8.2-jdk-8-slim AS stage1
WORKDIR /home/app
COPY . /home/app/
RUN mvn -f /home/app/pom.xml clean package

# Create an Image
FROM openjdk:8-jdk-alpine
EXPOSE 5000
COPY --from=stage1 /home/app/target/hello-world-java.jar hello-world-java.jar
ENTRYPOINT ["sh", "-c", "java -jar /hello-world-java.jar"]

#This Dockerfile creates a Docker image for a Java application. The application code is built using Maven in the first stage, and the resulting JAR file is then copied to the second stage which runs a minimal Alpine-based OpenJDK 8 container.
#Here is a breakdown of the steps in the Dockerfile:

#FROM maven:3.8.2-jdk-8-slim AS stage1: This starts the first stage of the multi-stage build process, using a slim version of Maven 3.8.2 with OpenJDK 8 as the base image.

#WORKDIR /home/app: Sets the working directory to /home/app in the container.

#COPY . /home/app/: Copies the contents of the current directory (presumably the source code for the Java application) to /home/app in the container.

#RUN mvn -f /home/app/pom.xml clean package: Runs the Maven clean and package goals on the pom.xml file located in /home/app directory, producing a JAR file with the compiled Java code in the /home/app/target directory.

#FROM openjdk:8-jdk-alpine: This starts the second stage of the build process, using a minimal Alpine-based OpenJDK 8 image as the base image.

#EXPOSE 5000: Exposes port 5000 on the container.

#COPY --from=stage1 /home/app/target/hello-world-java.jar hello-world-java.jar: Copies the JAR file produced in the first stage from /home/app/target directory to the root directory in the second stage.

#ENTRYPOINT ["sh", "-c", "java -jar /hello-world-java.jar"]: Sets the command to be run when the container starts. This command starts a shell and runs the Java program with the JAR file located at /hello-world-java.jar.
