# 🚀 Enterprise CI Pipeline with Jenkins, SonarQube & Nexus Repository on AWS

![Jenkins](https://img.shields.io/badge/Jenkins-CI/CD-red)
![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![SonarQube](https://img.shields.io/badge/SonarQube-Code%20Quality-blue)
![Nexus](https://img.shields.io/badge/Nexus-Artifact%20Repository-2C8EBB)
![Maven](https://img.shields.io/badge/Maven-Build-blue)
![Java](https://img.shields.io/badge/Java-OpenJDK%2017-orange)
![GitHub](https://img.shields.io/badge/GitHub-VersionControl-black)
![Pipeline](https://img.shields.io/badge/Jenkins-Pipeline%20as%20Code-red)
![DevOps](https://img.shields.io/badge/DevOps-Automation-green)

## 📖 Project Overview

This project demonstrates the implementation of an enterprise-grade Continuous Integration (CI) pipeline for the VProfile Java web application using *Jenkins Pipeline as Code* on Amazon Web Services (AWS).

The pipeline automates the software build lifecycle by retrieving source code from a Git repository, compiling the application with Apache Maven, performing static code analysis with Checkstyle, analyzing code quality using SonarQube, enforcing a Quality Gate, generating a deployable WAR artifact, archiving the build output, and publishing versioned artifacts to a Nexus Repository Manager.

The CI workflow was implemented using a Jenkins Pipeline script configured directly within Jenkins. The pipeline executed the Maven deployment command:

text
mvn clean deploy -DskipTests --settings /var/lib/jenkins/.m2/settings.xml


Upon successful execution, Jenkins produced a *BUILD SUCCESS* status and automatically published the generated artifacts, including the WAR package, POM file, Maven metadata, and checksum files, to the configured Nexus repository.

This project demonstrates practical experience in Continuous Integration (CI), Pipeline as Code, build automation, artifact management, static code analysis, and enterprise DevOps practices using AWS-hosted infrastructure.


## 🎯 Business Objective

The primary objective of this project was to design and implement an enterprise-grade Continuous Integration (CI) pipeline that automates the software build and quality assurance process for a Java web application.

The solution was developed to eliminate manual build activities by integrating source code management, automated compilation, static code analysis, quality gate validation, artifact generation, and centralized artifact storage into a single, repeatable pipeline.

By incorporating Jenkins Pipeline as Code, SonarQube, Maven, Checkstyle, and Nexus Repository Manager, the project demonstrates how modern DevOps practices improve software quality, build consistency, release readiness, and development efficiency while supporting scalable and reliable CI workflows on AWS infrastructure.


## 🏗️ Solution Architecture

The solution implements an enterprise-style Continuous Integration (CI) pipeline using Jenkins Pipeline as Code, SonarQube, Nexus Repository Manager, and AWS EC2 infrastructure. The pipeline automates source code retrieval, application build, code quality inspection, artifact generation, and artifact publishing while distributing responsibilities across dedicated infrastructure components.

---

### Architecture Diagram

text
                           Developer
                               │
                               ▼
                     GitHub Repository
                         (local branch)
                               │
                               ▼
          Jenkins Controller (AWS EC2 - Amazon Linux 2023)
                               │
                               ▼
                 Jenkins Pipeline (Pipeline as Code)
                               │
                               ▼
              Maven Build Agent (AWS EC2 - Ubuntu)
                               │
        ┌──────────────────────┼──────────────────────┐
        ▼                      ▼                      ▼
 Source Code Build       Checkstyle Analysis     Unit Tests
        │
        ▼
 SonarQube Server (AWS EC2 - Ubuntu 24.04)
        │
 PostgreSQL Database
        │
        ▼
 Quality Gate Validation
        │
        ▼
 WAR Artifact Generation
        │
        ▼
 Artifact Archiving
        │
        ▼
 Nexus Repository Manager
 (AWS EC2 - Amazon Linux 2023)
        │
        ▼
 BUILD SUCCESS


---

### Architecture Components

#### GitHub Repository
Hosts the VProfile Java application source code. Jenkins retrieves the latest code from the *local* branch before initiating the pipeline.

#### Jenkins Controller
Runs on an Amazon Linux 2023 EC2 instance and orchestrates the entire CI pipeline, including source code checkout, pipeline execution, build coordination, and integration with external DevOps tools.

#### Maven Build Agent
A dedicated Jenkins Agent (maven-agent) responsible for executing Maven build tasks, allowing build workloads to be distributed away from the Jenkins Controller.

#### SonarQube Server
Deployed on an Ubuntu 24.04 EC2 instance to perform static code analysis, evaluate code quality, detect bugs and code smells, and enforce Quality Gate validation before artifact publication.

#### PostgreSQL Database
Installed on the same EC2 instance as SonarQube to provide persistent storage for project analysis data, quality metrics, and historical scan results.

#### Nexus Repository Manager
Hosted on an Amazon Linux 2023 EC2 instance to centrally store versioned Maven artifacts, including WAR files, POM files, metadata, and checksum files generated by the pipeline.

#### Nginx Reverse Proxy
Configured in front of the SonarQube server to provide secure and reliable HTTP access while acting as a reverse proxy for incoming client requests.

---

### Solution Flow

1. Developer pushes source code to the GitHub repository.
2. Jenkins Pipeline checks out the *local* branch from GitHub.
3. The pipeline dispatches the build to the dedicated *maven-agent*.
4. Maven compiles the application and resolves project dependencies.
5. Unit tests and Checkstyle analysis are executed.
6. SonarQube performs static code analysis and evaluates the configured Quality Gate.
7. Upon successful validation, Jenkins generates and archives the WAR artifact.
8. The pipeline publishes the versioned artifacts to the Nexus Repository Manager.
9. Jenkins reports a final *BUILD SUCCESS*, confirming successful completion of the CI workflow.
