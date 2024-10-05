pipeline {
    agent any

    environment {
        BUILD_AUTOMATION_TOOL = "Maven"
        UNIT_TEST_TOOL = "JUnit"
        INTEGRATION_TEST_TOOL = "Protractor"
        ANALYSE_TOOL = "FindBug"
        SECURITY_SCAN = "Checkmarx"
        SERVER = "AWS EC2 instance"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the code using ${env.BUILD_AUTOMATION_TOOL} to compile and package."
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests with ${env.UNIT_TEST_TOOL} to ensure code functionality."
                echo "Running integration tests with ${env.INTEGRATION_TEST_TOOL} to validate system components."
            }
            post {
                success {
                    emailNotification("Unit and Integration Test Status", "Unit and Integration Tests were successful!")
                }
                failure {
                    emailNotification("Unit and Integration Test Status", "Unit and Integration Tests failed!")
                }
            }
        }

        stage('Code Check') {
            steps {
                echo "Analyzing code with ${env.ANALYSE_TOOL} to ensure industry standards."
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan with ${env.SECURITY_SCAN} to identify vulnerabilities."
            }
            post {
                success {
                    emailNotification("Security Scan Status", "Security Scan was successful!")
                }
                failure {
                    emailNotification("Security Scan Status", "Security Scan failed!")
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to ${env.SERVER} for staging."
                sleep 10
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging environment."
            }
            post {
                success {
                    emailNotification("Integration Tests on Staging Status", "Integration Tests on Staging were successful!")
                }
                failure {
                    emailNotification("Integration Tests on Staging Status", "Integration Tests on Staging failed!")
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to ${env.SERVER} for production."
            }
        }
    }
}

def emailNotification(subject, body) {
    emailext(
        to: "muskkann.20@gmail.com",
        subject: subject,
        body: body,
        attachLog: true
    )
}
