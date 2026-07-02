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
