pipeline {
    agent any

    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'kwarimasimba@gmail.com'
        LOG_FILE = "pipeline-log-${env.BUILD_ID}.txt"
    }

    triggers {
        // This schedule will trigger the pipeline every day at midnight (00:00).
        cron('H 0 * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                echo 'Build tool: Maven'
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Building the code...' >> ${env.LOG_FILE}"
                        sh "echo 'Build tool: Maven' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Building the code... >> ${env.LOG_FILE}"
                        bat "echo Build tool: Maven >> ${env.LOG_FILE}"
                    }
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Test tools: JUnit, Selenium'
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Running unit and integration tests...' >> ${env.LOG_FILE}"
                        sh "echo 'Test tools: JUnit, Selenium' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Running unit and integration tests... >> ${env.LOG_FILE}"
                        bat "echo Test tools: JUnit, Selenium >> ${env.LOG_FILE}"
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality...'
                echo 'Code analysis tool: SonarQube'
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Analyzing code quality...' >> ${env.LOG_FILE}"
                        sh "echo 'Code analysis tool: SonarQube' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Analyzing code quality... >> ${env.LOG_FILE}"
                        bat "echo Code analysis tool: SonarQube >> ${env.LOG_FILE}"
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                echo 'Security scan tool: OWASP Dependency Check'
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Performing security scan...' >> ${env.LOG_FILE}"
                        sh "echo 'Security scan tool: OWASP Dependency Check' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Performing security scan... >> ${env.LOG_FILE}"
                        bat "echo Security scan tool: OWASP Dependency Check >> ${env.LOG_FILE}"
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                echo "Deploying to ${env.STAGING_SERVER}"
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Deploying to staging environment...' >> ${env.LOG_FILE}"
                        sh "echo 'Deploying to ${env.STAGING_SERVER}' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Deploying to staging environment... >> ${env.LOG_FILE}"
                        bat "echo Deploying to ${env.STAGING_SERVER} >> ${env.LOG_FILE}"
                    }
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Running integration tests on staging...' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Running integration tests on staging... >> ${env.LOG_FILE}"
                    }
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                echo "Deploying to ${env.PRODUCTION_SERVER}"
                // Save logs to a file
                script {
                    if (isUnix()) {
                        sh "echo 'Deploying to production environment...' >> ${env.LOG_FILE}"
                        sh "echo 'Deploying to ${env.PRODUCTION_SERVER}' >> ${env.LOG_FILE}"
                    } else {
                        bat "echo Deploying to production environment... >> ${env.LOG_FILE}"
                        bat "echo Deploying to ${env.PRODUCTION_SERVER} >> ${env.LOG_FILE}"
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed with status: ' + currentBuild.currentResult

            // Attach the log file to the email
            emailext (
                to: "${env.RECIPIENT_EMAIL}",
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: """The pipeline has completed with status: ${currentBuild.currentResult}.
                Please find the attached logs for more details.""",
                attachmentsPattern: "${env.LOG_FILE}",
                mimeType: 'text/plain'
            )

            // Clean up the log file after sending the email
            script {
                if (isUnix()) {
                    sh "rm -f ${env.LOG_FILE}"
                } else {
                    bat "del ${env.LOG_FILE}"
                }
            }
        }
    }
}
