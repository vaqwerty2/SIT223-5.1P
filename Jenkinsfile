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
                script {
                    echo "Building the application..."
                    echo 'Using a build automation tool like Maven or Gradle to compile and package the code.'
                    // Example: sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Running Unit and Integration Tests..."
                    echo 'Using a test automation tool like JUnit for unit tests and TestNG for integration tests.'
                    // Example: sh 'mvn test'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo "Performing Code Analysis..."
                    echo 'Using a basic tool like Checkstyle or PMD to analyze the code quality.'
                    // Example: sh 'checkstyle -c /google_checks.xml MyClass.java'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo "Running Security Scan..."
                    echo 'Using a basic tool like OWASP Dependency Check to identify vulnerabilities.'
                    // Example: sh 'dependency-check --project MyApp --scan .'
                }
            }
            post {
                success {
                    script {
                        emailext to: 'vidulattri2003@gmail.com',
                                 subject: "Security Scan Passed - Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                                 body: """The security scan in pipeline ${env.JOB_NAME} completed successfully.

Check the results here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                                 attachLog: true
                    }
                }
                failure {
                    script {
                        emailext to: 'vidulattri2003@gmail.com',
                                 subject: "Security Scan Failed - Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                                 body: """The security scan in pipeline ${env.JOB_NAME} has failed.

Check the details here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                                 attachLog: true
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying the application to the Staging environment..."
                    echo 'Deploying using a script or tool like SCP to transfer files to a staging server.'
                    // Example: sh 'scp target/myapp.jar user@staging_server:/path/to/deploy/'
                    // Example: sh 'ssh user@staging_server "bash /path/to/deploy.sh"'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Running Integration Tests on the Staging environment..."
                    echo 'Using the same tools as the unit and integration test stage to validate the deployment.'
                    // Example: sh 'ssh user@staging_server "bash /path/to/tests/integration_tests.sh"'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying the application to the Production environment..."
                    echo 'Deploying using a script or tool like SCP to transfer files to a production server.'
                    // Example: sh 'scp target/myapp.jar user@production_server:/path/to/deploy/'
                    // Example: sh 'ssh user@production_server "bash /path/to/deploy.sh"'
                }
            }
        }
    }

    post {
        success {
            script {
                emailext to: 'vidulattri2003@gmail.com',
                         subject: "Pipeline ${env.JOB_NAME} - ${env.BUILD_NUMBER} Success",
                         body: """The pipeline ${env.JOB_NAME} completed successfully.

Check the results here: ${env.BUILD_URL}

Commit Message:
${COMMIT_MESSAGE}""",
                         attachLog: true
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
                         attachLog: true
            }
        }
    }
}
