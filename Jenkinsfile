pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Initiating the build process: compiling and packaging the code using an automation tool."
                echo "Build Tool: Maven"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Executing unit tests to validate individual components and integration tests to verify overall functionality."
                echo "Test Tools: JUnit for unit tests, Selenium for integration testing"
            }
            post {
                success {
                    emailext subject: "Success - Unit and Integration Tests",
                             body: "All unit and integration tests were completed successfully.",
                             to: 'kwarimasimba@gmail.com',
                             attachLog: true
                }
                failure {
                    emailext subject: "Failure - Unit and Integration Tests",
                             body: "Some of the unit or integration tests failed. Please review the logs.",
                             to: 'kwarimasimba@gmail.com',
                             attachLog: true
                }
            }
        }

        stage('Code Quality Analysis') {
            steps {
                echo "Performing static code analysis to check for quality and adherence to standards."
                echo "Analysis Tool: SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Running a security scan to identify any potential vulnerabilities in the application."
                echo "Security Tool: OWASP Dependency-Check"
            }
            post {
                success {
                    emailext subject: "Success - Security Scan",
                             body: "The security scan completed with no issues found.",
                             to: 'kwarimasimba@gmail.com',
                             attachLog: true
                }
                failure {
                    emailext subject: "Failure - Security Scan",
                             body: "The security scan found vulnerabilities. Please review the report for details.",
                             to: 'kwarimasimba@gmail.com',
                             attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging environment for further validation in a near-production setup."
                echo "Deployment Tool: AWS EC2"
            }
        }

        stage('Integration Tests in Staging') {
            steps {
                echo "Running comprehensive integration tests in the staging environment to simulate real-world usage."
                echo "Test Tools: Postman for API testing, Selenium for UI validation"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the finalized application to the production environment, making it live for users."
                echo "Deployment Tool: AWS EC2"
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed."
        }
    }
}
