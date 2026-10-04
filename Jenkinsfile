// SIT753 7.1C - 7-stage pipeline with email notifications (Part 2 Task 2)

def sendStageEmail(String stageName, String status) {
    emailext(
        to: env.EMAIL_TO,
        subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} - ${stageName}: ${status}",
        body: """Stage: ${stageName}
Status: ${status}
Job: ${env.JOB_NAME}
Build number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}

The build log up to this stage is attached.""",
        attachLog: true
    )
}

pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')
    }

    environment {
        EMAIL_TO = 'sathsarnisayuri@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: compile the source code and package it into a deployable artifact (JAR).'
                echo 'Tool: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: run unit tests on individual components and integration tests to check the components work together.'
                echo 'Tools: JUnit (unit tests) and Selenium (integration tests)'
            }
            post {
                success { sendStageEmail('Unit and Integration Tests', 'SUCCESS') }
                failure { sendStageEmail('Unit and Integration Tests', 'FAILURE') }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: analyse the code for bugs, code smells and maintainability against industry standards.'
                echo 'Tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: scan the code and its third-party dependencies for known vulnerabilities (CVEs).'
                echo 'Tool: OWASP Dependency-Check'
            }
            post {
                success { sendStageEmail('Security Scan', 'SUCCESS') }
                failure { sendStageEmail('Security Scan', 'FAILURE') }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: deploy the packaged application to the staging server (AWS EC2 instance).'
                echo 'Tool: Ansible'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: run integration tests against staging to confirm the application works in a production-like environment.'
                echo 'Tool: Postman/Newman'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: deploy the verified application to the production server (AWS EC2 instance).'
                echo 'Tool: Ansible'
            }
        }
    }

    post {
        always {
            echo "Pipeline finished with status: ${currentBuild.currentResult}"
        }
    }
}
