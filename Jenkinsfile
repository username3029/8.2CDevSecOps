pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from repository
                git branch: 'main', url: 'https://github.com/your_github_username/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // If running natively on Windows Jenkins, you can use: bat 'npm install'
                // If running inside Docker (Linux), use: sh 'npm install'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Allows pipeline to continue despite test failures
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                // Ensure coverage report exists
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                // Runs security scan and outputs known CVEs into the console log
                sh 'npm audit || true'
            }
        }
    }

    post {
        always {
            // Part 2 Task 2: Extended Email Plugin notification with attached logs
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
                to: 'your_email@example.com',
                attachLog: true,
                compressLog: true
            )
        }
    }
}
