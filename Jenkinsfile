pipeline {
    agent any

    environment {
        COMMIT_MESSAGE = '' // Variable to store the commit message
        LOG_FILE = 'pipeline_log.txt' // Log file to store logs
        CONSOLE_LOG = 'console_output.txt' // File to store the console output
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout and fetch the latest commit message
                    checkout scm
                    COMMIT_MESSAGE = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()
                    echo "Commit Message: ${COMMIT_MESSAGE}"
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    def log = "Building the application...\n"
                    log += 'Using a build automation tool like Maven or Gradle to compile and package the code (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Running Unit and Integration Tests (Mock)...\n"
                    log += 'Using JUnit/TestNG (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Performing Code Analysis (Mock)...\n"
                    log += 'Using Checkstyle/PMD (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Running Security Scan (Mock)...\n"
                    log += 'Using OWASP Dependency Check (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Deploying the application to the Staging environment (Mock)...\n"
                    log += 'Using SCP or a similar tool (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Running Integration Tests on the Staging environment (Mock)...\n"
                    log += 'Using JUnit/TestNG (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    def log = readFile(file: "${LOG_FILE}")
                    log += "Deploying the application to the Production environment (Mock)...\n"
                    log += 'Using SCP or a similar tool (Mock).\n'
                    writeFile file: "${LOG_FILE}", text: log
                    echo log
                }
            }
        }
    }

    post {
        always {
            script {
                // Capture console output within sandbox
                def consoleOutput = sh(script: 'cat $BUILD_LOG', returnStdout: true).trim()
                writeFile file: "${CONSOLE_LOG}", text: consoleOutput

                // Archive the console output and the log file
                archiveArtifacts artifacts: "${LOG_FILE}, ${CONSOLE_LOG}", allowEmptyArchive: true
            }
        }
        success {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Success",
                         body: """The pipeline ${env.JOB_NAME} completed successfully.

Commit Message:
${COMMIT_MESSAGE}

Check the full console output in the attached file.""",
                         attachmentsPattern: "${CONSOLE_LOG}"
            }
        }
        failure {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Failed",
                         body: """The pipeline ${env.JOB_NAME} failed.

Commit Message:
${COMMIT_MESSAGE}

Check the full console output in the attached file.""",
                         attachmentsPattern: "${CONSOLE_LOG}"
            }
        }
    }
}

// Post action for email notification after Security Scan stage
post {
    stage('Security Scan') {
        success {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Security Scan Passed",
                         body: """The Security Scan for pipeline ${env.JOB_NAME} completed successfully.

Commit Message:
${COMMIT_MESSAGE}

Check the full console output in the attached file.""",
                         attachmentsPattern: "${CONSOLE_LOG}"
            }
        }
        failure {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Security Scan Failed",
                         body: """The Security Scan for pipeline ${env.JOB_NAME} failed.

Commit Message:
${COMMIT_MESSAGE}

Check the full console output in the attached file.""",
                         attachmentsPattern: "${CONSOLE_LOG}"
            }
        }
    }
}
