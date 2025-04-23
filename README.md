# AWS Hello World - Java Spring Boot with Jenkins CI/CD

## Overview

This project demonstrates a simple *Hello World* application built using *Java Spring Boot* and deployed using *Jenkins CI/CD pipeline* on *AWS*. It provides an example of integrating Jenkins with a Spring Boot app for continuous integration and deployment, using best practices for modern DevOps.

## Features

- Simple *Java Spring Boot* application that displays a "Text" message which you declared in controller.java file.
- *CI/CD pipeline* using Jenkins to automate builds, test and picturize the docker.
- Published the docker image into docker hub.

## Technologies Used

- *Java 11* for the backend.
- *Spring Boot* framework.
- *Jenkins* for CI/CD pipeline.
- *AWS EC2* for hosting the application.
- *Docker* for containerization.
- *GitHub* for version control.

## Setup and Installation

### Prerequisites
Before you begin, ensure you have the following installed in AWS EC2:
- Java 11 or higher
- Maven
- Jenkins (for CI/CD)
- Docker

### Steps
1. Create the app by usingSpring Initializr (GUI)
- Visit [https://start.spring.io/](https://start.spring.io/)
- Choose the following options:
  - *Project*: Maven
  - *Language*: Java
  - *Spring Boot Version*: 2.7.x or 3.x
  - *Group*: com.est
  - *Artifact*: aws-hello-world
  - *Dependencies*: Spring Web

- Click *Generate*, unzip the project, and open it in your IDE.
---------------------------------------------------------------------------
Now we build with maven
./mvnw clean package
  we can see the below message 
[INFO] BUILD SUCCESS

  ----------------------------------------------------------------------------
Now your Spring Boot app is ready to be Dockerized.
#Step 1: Create a Dockerfile
We have to create Dockerfile in your project root (~/projects/hello-world):

#Step 2: Build the Docker Image
Now run:
    docker build -t hello-world-app .
we could see below context
Successfully tagged hello-world-app:latest

#Step 3: verify the image is built or not
now run:
    docker images

#Step 4: Run it in a container
    docker run -d -p 8081:8080 --name hello-world-app hello-world-app
then it shows like 
ea45477ad5a4eba6bf664ba1b1f1a2e377ca17dddd95185b6f642cc22b8ebc34

#Step 5: Check it in browser
    Open browser and type http://ec2publicip:8081 
it shows our hellocontroller.java return message
I showcased the app in browser with this line "Powerful comeback- HEY EC2!"

--------------------------------------------------------------------------------
Pre check about Jenkins Installation 
Start and Enable Jenkins
    sudo systemctl start jenkins
    sudo systemctl enable jenkins
Check Jenkins Status
    sudo systemctl status jenkins

Phase 2: Access Jenkins from Browser
Let’s open Jenkins UI and unlock it.

#Configure the Job
1. Source Code Management (We can do it later also)
Choose Git
Enter your GitHub repo URL:
https://github.com/your-username/your-repo.git
Add credentials if your repo is private.
Branch (optional)
Default: */main
Change if needed

2. Triggers
tick the GitHub hook trigger for GITScm polling
It is needed when we are going to push thw job automatically github using webhook method.

3. Build Environment (optional)
Check this if needed:
Delete workspace before build starts – to clean old files

4. Build Steps 
Choose Execute Shell in Add build step
and enter as command as your wish
We choosed to dockerize the image automatically

5. Save the changes and back to the 
Then click “Build Now” in left side menu.
We can see the build job in bottom of the left side 
We can choose the console output to monitor the real-time logs 

# Project Structure

src/main/java: Java source files for the Spring Boot app.

src/main/resources: Application properties and other resources.

pom.xml: Maven build file.

DockerFile: Docker source file for built the docker image

# CI/CD Pipeline

The Jenkins pipeline automates the following steps:

Code Compilation using Maven.

Docker Image Build.

Automate Docker image creation and push to DockerHub via Jenkins. 


#Future Enhancement
- *Kubernetes Deployment:* Deploy to a Kubernetes cluster with Helm or manifests.
- *GitHub Webhook Integration:* Automatically trigger Jenkins pipeline on GitHub code pushes.
- *Infrastructure as Code (IaC):* Use Terraform or Ansible for automated AWS infrastructure setup.
- *Monitoring & Logging:* Integrate Prometheus, Grafana, and ELK stack for observability.


Thank you for using this project!
Feel free to contribute or suggest improvements.
Happy Coding! 🎉

