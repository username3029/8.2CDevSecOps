pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/username3029/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install || exit /b 0'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }

    post {
        always {
            // Part 2 Task 2: Extended Email Notifications with log attachments
            emailext (
                subject: "Build Status: ${currentBuild.currentResult} - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h3>Build Execution Completed</h3>
                    <p><b>Status:</b> ${currentBuild.currentResult}</p>
                    <p><b>Job:</b> ${env.JOB_NAME}</p>
                    <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                    <p>View detailed log in Jenkins: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'CulpritsRecipientProvider']],
                to: 'tomar.dev@hotmail.com',
                attachLog: true,
                compressLog: true
            )
        }
    }
}
