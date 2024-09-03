pipeline {
    agent any

    environment {
        COMMIT_MESSAGE = '' // Variable to store the commit message
        LOG_FILE = 'pipeline_log.txt' // Log file to store logs
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
                script {
                    def log = "Building the application...\n"
                    log += 'Using a build automation tool like Maven or Gradle to compile and package the code.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Running Unit and Integration Tests...\n"
                    log += 'Using a test automation tool like JUnit for unit tests and TestNG for integration tests.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'mvn test'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Performing Code Analysis...\n"
                    log += 'Using a basic tool like Checkstyle or PMD to analyze the code quality.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'checkstyle -c /google_checks.xml MyClass.java'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Running Security Scan...\n"
                    log += 'Using a basic tool like OWASP Dependency Check to identify vulnerabilities.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'dependency-check --project MyApp --scan .'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Deploying the application to the Staging environment...\n"
                    log += 'Deploying using a script or tool like SCP to transfer files to a staging server.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'scp target/myapp.jar user@staging_server:/path/to/deploy/'
                    // Example: sh 'ssh user@staging_server "bash /path/to/deploy.sh"'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Running Integration Tests on the Staging environment...\n"
                    log += 'Using the same tools as the unit and integration test stage to validate the deployment.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'ssh user@staging_server "bash /path/to/tests/integration_tests.sh"'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Deploying the application to the Production environment...\n"
                    log += 'Deploying using a script or tool like SCP to transfer files to a production server.\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                    // Example: sh 'scp target/myapp.jar user@production_server:/path/to/deploy/'
                    // Example: sh 'ssh user@production_server "bash /path/to/deploy.sh"'
                }
            }
        }
    }

    post {
        always {
            script {
                // Ensure the log file is archived so it can be attached to the email
                archiveArtifacts artifacts: "${LOG_FILE}", allowEmptyArchive: true
            }
        }
        success {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Success",
                         body: """The pipeline ${env.JOB_NAME} completed successfully.

Check the results here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                         attachmentsPattern: "${LOG_FILE}"
            }
        }
        failure {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Failed",
                         body: """The pipeline ${env.JOB_NAME} has failed.

Check the details here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                         attachmentsPattern: "${LOG_FILE}"
            }
        }
    }
}
