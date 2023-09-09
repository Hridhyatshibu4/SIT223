pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Use Maven or your preferred build tool to compile and package the code.
                script {
                    // Adjust the command for Windows using 'start /B'
                    if (isUnix()) {
                        sh 'mvn clean install'
                    } else {
                        bat 'start /B mvn clean install' // Use 'bat' on Windows
                    }
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                // Run unit and integration tests using appropriate test automation tools.
                script {
                    if (isUnix()) {
                        sh 'npm install'
                        sh 'npm test'
                    } else {
                        bat 'start /B npm install'
                        bat 'start /B npm test'
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool like SonarQube or Checkstyle.
                script {
                    if (isUnix()) {
                        sh 'sonar-scanner'
                    } else {
                        bat 'start /B sonar-scanner'
                    }
                }
            }
        }
        stage('Security Scan') {
            steps {
                // Perform security scanning using a security tool like OWASP ZAP or Snyk.
                script {
                    if (isUnix()) {
                        sh 'owasp-zap-scan'
                    } else {
                        bat 'start /B owasp-zap-scan'
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Deploy to your staging environment (e.g., AWS EC2).
                script {
                    if (isUnix()) {
                        sh 'aws deploy-staging'
                    } else {
                        bat 'start /B aws deploy-staging'
                    }
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on the staging environment.
                script {
                    if (isUnix()) {
                        sh 'npm run integration-test'
                    } else {
                        bat 'start /B npm run integration-test'
                    }
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                // Deploy to your production environment (e.g., AWS EC2).
                script {
                    if (isUnix()) {
                        sh 'aws deploy-production'
                    } else {
                        bat 'start /B aws deploy-production'
                    }
                }
            }
        }
    }
    post {
        failure {
            emailext subject: "Pipeline Failed",
                body: "The Jenkins pipeline has failed. Please check the logs for details.",
                to: 'davenair1@gmail.com'
        }
        success {
            emailext subject: "Pipeline Successful",
                body: "The Jenkins pipeline has succeeded.",
                to: 'davenair1@gmail.com'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
