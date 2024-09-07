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
        post {
            success {
                emailext (
                    to: "vidulattri2003@gmail.com",
                    subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Security Scan Passed",
                    body: """The pipeline ${env.JOB_NAME} has passed the Security Scan.

Commit Message:
${COMMIT_MESSAGE}

Check the attached console log.""",
                    attachLog: true
                )
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
                // Archive the log file
                archiveArtifacts artifacts: "${LOG_FILE}", allowEmptyArchive: true
            }
        }
        success {
            emailext (
                to: "vidulattri2003@gmail.com",
                subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Success",
                body: """The pipeline ${env.JOB_NAME} completed successfully.

Commit Message:
${COMMIT_MESSAGE}

Check the attached console log.""",
                attachLog: true
            )
        }
        failure {
            emailext (
                to: "vidulattri2003@gmail.com",
                subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Failed",
                body: """The pipeline ${env.JOB_NAME} has failed.

Commit Message:
${COMMIT_MESSAGE}

Check the attached console log.""",
                attachLog: true
            )
        }
    }
}
