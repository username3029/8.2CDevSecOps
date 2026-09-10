pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/username3029/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm install'
                    } else {
                        bat 'npm install'
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm test || true'
                    } else {
                        bat 'npm test || exit /b 0'
                    }
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm run coverage || true'
                    } else {
                        bat 'npm run coverage || exit /b 0'
                    }
                }
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm audit || true'
                    } else {
                        bat 'npm audit || exit /b 0'
                    }
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Build Status [${currentBuild.currentResult}] - Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Execution Summary</h2>
                    <p><b>Job Name:</b> ${env.JOB_NAME}</p>
                    <p><b>Build Number:</b> #${env.BUILD_NUMBER}</p>
                    <p><b>Result:</b> ${currentBuild.currentResult}</p>
                    <p>View complete build details in Jenkins: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'CulpritsRecipientProvider']],
                to: 'tomar.dev@hotmail.com',
                attachLog: true,
                compressLog: true
            )
        }
    }
}
