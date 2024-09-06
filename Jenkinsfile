pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Compiling the code using a build automation tool to compile and package the code."
                echo "Tool: Maven"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests to verify code functionality and integration tests to ensure all components work together."
                echo "Tools: JUnit (for unit tests), Selenium (for integration tests)"
            }
            post {
                success {
                    emailext subject: "Build Successful - Unit and Integration Tests",
                             body: "The unit and integration tests passed successfully.",
                             to: 'kwarimasimba@gmail.com',
                             attachLog: true
                }
                failure {
                    emailext subject: "Build Failed - Unit and Integration Tests",
                             body: "The unit and integration tests failed.",
                             to: 'kwarimasimba@gmail.com',
                             attachLog: true
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Running static code analysis to ensure code quality and adherence to industry standards."
                echo "Tool: SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing a security scan to identify potential vulnerabilities in the code and dependencies."
                echo "Tool: OWASP Dependency-Check"   
            }
                post {
                    success {
                        emailext subject: "Build Successful - Security Scan",
                                 body: "The security scan passed successfully.",
                                 to: 'kwarimasimba@gmail.com',
                                 attachLog: true
                }
                    failure {
                        emailext subject: "Build Failed - Security Scan",
                                 body: "The security scan failed.",
                                 to: 'kwarimasimba@gmail.com',
                                 attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to a staging server for further testing in a production-like environment."
                echo "Tool: AWS EC2"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment to ensure the application functions as expected."
                echo "Tools: Postman (for API tests), Selenium (for UI tests)"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to a production environment, making it available to end users."
                echo "Tool: AWS EC2"
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
        }
    }
}
