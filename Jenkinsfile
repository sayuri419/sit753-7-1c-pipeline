pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven to compile the source code and package it into a deployable artifact (e.g. a JAR file).'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit to verify individual components, and integration tests with Selenium to confirm the application modules work together correctly.'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analysing the code with SonarQube to check for code smells, maintainability issues, and adherence to coding standards.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning the codebase and its dependencies with OWASP Dependency-Check to identify known vulnerabilities (CVEs) in third-party libraries.'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the packaged application to a staging server (an AWS EC2 instance) using Ansible for automated configuration.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests against the staging environment with Postman/Newman to confirm the application behaves correctly in a production-like setting.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the verified application to the production server (an AWS EC2 instance) using Ansible.'
            }
        }
    }
}
