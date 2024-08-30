# Java Blogging App Deployment Pipeline

This repository contains the CI/CD pipeline configuration for deploying a Java blogging application. The pipeline utilizes Jenkins, Docker, SonarQube, and Nexus, with Terraform managing the deployment of the Kubernetes app to the AWS platform.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Pipeline Overview](#pipeline-overview)
- [Setup Instructions](#setup-instructions)
  - [Jenkins Setup](#jenkins-setup)
  - [SonarQube Setup](#sonarqube-setup)
  - [Nexus Setup](#nexus-setup)
  - [Terraform Setup](#terraform-setup)
- [Running the Pipeline](#running-the-pipeline)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

- Java Development Kit (JDK)
- Docker
- Jenkins
- SonarQube
- Nexus Repository Manager
- Terraform
- AWS Account

## Pipeline Overview

The deployment pipeline includes the following stages:

1. **Code Checkout**: Retrieve the latest code from the Git repository.
2. **Build and Test**: Compile the Java application and run unit tests.
3. **Code Analysis**: Perform static code analysis using SonarQube.
4. **Build Docker Image**: Create a Docker image of the application.
5. **Push Docker Image to Nexus**: Store the Docker image in Nexus Repository Manager.
6. **Deploy to Kubernetes**: Use Terraform to deploy the application to an AWS-managed Kubernetes cluster.

## Setup Instructions

### Jenkins Setup

1. Install Jenkins and required plugins (Git, Docker, SonarQube Scanner, etc.).
2. Create a new Jenkins pipeline and link it to your Git repository: `https://github.com/web081/java-blogging-app-pipeline-ci-cd/`.
3. Configure Jenkins to use Docker for building and deploying images.
4. Set up SonarQube and Nexus credentials in Jenkins.

### SonarQube Setup

1. Install and configure SonarQube.
2. Create a new project in SonarQube.
3. Generate a project token and configure it in Jenkins.

### Nexus Setup

1. Install and configure Nexus Repository Manager.
2. Create a new Docker registry in Nexus.
3. Set up Nexus credentials in Jenkins.

### Terraform Setup

1. Install Terraform.
2. Configure AWS credentials for Terraform.
3. Update the Terraform scripts in the `terraform/` directory with your AWS configuration.

## Running the Pipeline

1. Push your code changes to the Git repository.
2. The Jenkins pipeline will automatically start and perform the following tasks:
   - Checkout the code
   - Build and test the application
   - Analyze the code with SonarQube
   - Build a Docker image
   - Push the Docker image to Nexus
   - Deploy the application to AWS Kubernetes using Terraform

## Project Structure


- `Jenkinsfile`: Jenkins pipeline script.
- `Dockerfile`: Docker configuration for building the application image.
- `sonar-project.properties`: SonarQube project configuration.
- `terraform/`: Terraform scripts for deploying the application to AWS Kubernetes.
- `src/`: Java source code and test files.
- `README.md`: Project documentation.




