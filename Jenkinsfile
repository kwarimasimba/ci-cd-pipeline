pipeline {
    agent any
    
    environment {
        DIRECTORY_PATH = '/path/to/code/directory'
        STAGING_SERVER = 'AWS Staging Server'
        PRODUCTION_SERVER = 'AWS Production Server'
        EMAIL_RECIPIENT = 'kwarimasimba@gmail.com' 
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                // Tool: Maven
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests and integration tests"
                // Tools: JUnit for unit tests, Selenium for integration tests
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Performing code analysis using SonarQube"
                // Tool: SonarQube
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP ZAP"
                // Tool: OWASP ZAP
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying application to ${env.STAGING_SERVER}"
                // Tool: Ansible or AWS CLI
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging environment"
                // Tools: Selenium for integration tests
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to ${env.PRODUCTION_SERVER}"
                // Tool: Ansible or AWS CLI
            }
        }
    }

    post {
        success {
            mail to: "${env.EMAIL_RECIPIENT}",
                 subject: "Jenkins Build Successful",
                 body: "The build completed successfully. Check Jenkins for full logs."
        }
        failure {
            mail to: "${env.EMAIL_RECIPIENT}",
                 subject: "Jenkins Build Failed",
                 body: "The build failed. Check Jenkins for full logs."
        }
    }
}
