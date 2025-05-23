pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/KaranNegi20Feb/Karan-Git-Learn'
            }
        }

        stage('Build and Run Tests') {
            steps {
                sh './gradlew clean test' // if using Gradle
                // OR if Maven
                // sh 'mvn clean test'
            }
        }

        stage('Publish ExtentReports') {
            steps {
                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'path/to/extentreport/output',
                    reportFiles: 'index.html',
                    reportName: 'Extent Report'
                ])
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Selenium Test Report - ${currentBuild.fullDisplayName}",
                body: "Test Report attached.\n\nBuild URL: ${env.BUILD_URL}",
                to: 'karanegi076@example.com',
                attachLog: true
            )
        }
    }
}
