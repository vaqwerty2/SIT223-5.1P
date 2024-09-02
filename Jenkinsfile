pipeline {
    agent any

    environment {
        COMMIT_MESSAGE = '' // Variable to store message
        LOG_FILE = 'pipeline.log' // Log file to store logs
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Ensure SCM checkout and then fetch the latest commit message
                    def scmVars = checkout scm
                    // Fetch the latest commit message
                    COMMIT_MESSAGE = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()
                    echo "Commit Message: ${COMMIT_MESSAGE}"
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...' | tee "${LOG_FILE}"
                echo 'Using a build automation tool like Maven or Gradle to compile and package the code.' | tee -a "${LOG_FILE}"
                // Example: sh 'mvn clean package' | tee -a "${LOG_FILE}"
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...' | tee -a "${LOG_FILE}"
                echo 'Using a test automation tool like JUnit for unit tests and TestNG for integration tests.' | tee -a "${LOG_FILE}"
                // Example: sh 'mvn test' | tee -a "${LOG_FILE}"
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...' | tee -a "${LOG_FILE}"
                echo 'Using a basic tool like Checkstyle or PMD to analyze the code quality.' | tee -a "${LOG_FILE}"
                // Example: sh 'checkstyle -c /google_checks.xml MyClass.java' | tee -a "${LOG_FILE}"
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...' | tee -a "${LOG_FILE}"
                echo 'Using a basic tool like OWASP Dependency Check to identify vulnerabilities.' | tee -a "${LOG_FILE}"
                // Example: sh 'dependency-check --project MyApp --scan .' | tee -a "${LOG_FILE}"
            }
            post {
                success {
                    echo 'Security scan passed successfully!' | tee -a "${LOG_FILE}"
                    mail to: 'vidulattri2003@gmail.com',
                         subject: "Security Scan Passed - Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                         body: """The security scan in pipeline ${env.JOB_NAME} completed successfully.

Check the results here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                         attachmentsPattern: "${LOG_FILE}"
                }
                failure {
                    echo 'Security scan failed!' | tee -a "${LOG_FILE}"
                    mail to: 'vidulattri2003@gmail.com',
                         subject: "Security Scan Failed - Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                         body: """The security scan in pipeline ${env.JOB_NAME} has failed.

Check the details here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                         attachmentsPattern: "${LOG_FILE}"
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the Staging environment...' | tee -a "${LOG_FILE}"
                echo 'Deploying using a script or tool like SCP to transfer files to a staging server.' | tee -a "${LOG_FILE}"
                // Example: sh 'scp target/myapp.jar user@staging_server:/path/to/deploy/' | tee -a "${LOG_FILE}"
                // Example: sh 'ssh user@staging_server "bash /path/to/deploy.sh"' | tee -a "${LOG_FILE}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on the Staging environment...' | tee -a "${LOG_FILE}"
                echo 'Using the same tools as the unit and integration test stage to validate the deployment.' | tee -a "${LOG_FILE}"
                // Example: sh 'ssh user@staging_server "bash /path/to/tests/integration_tests.sh"' | tee -a "${LOG_FILE}"
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the Production environment...' | tee -a "${LOG_FILE}"
                echo 'Deploying using a script or tool like SCP to transfer files to a production server.' | tee -a "${LOG_FILE}"
                // Example: sh 'scp target/myapp.jar user@production_server:/path/to/deploy/' | tee -a "${LOG_FILE}"
                // Example: sh 'ssh user@production_server "bash /path/to/deploy.sh"' | tee -a "${LOG_FILE}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!' | tee -a "${LOG_FILE}"
            mail to: 'vidulattri2003@gmail.com',
                 subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Success",
                 body: """The pipeline ${env.JOB_NAME} completed successfully.

Check the results here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                 attachmentsPattern: "${LOG_FILE}"
        }
        failure {
            echo 'Pipeline failed!' | tee -a "${LOG_FILE}"
            mail to: 'vidulattri2003@gmail.com',
                 subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Failed",
                 body: """The pipeline ${env.JOB_NAME} has failed.

Check the details here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                 attachmentsPattern: "${LOG_FILE}"
        }
    }
}
