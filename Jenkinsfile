pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'testNG',
            url: 'git@github.com:TripleDartPlatform/TripleDartQA_Automation.git',
            credentialsId: 'github-ssh'   // remove if public repo
      }
        }

        stage('Build & Run Cucumber Tests') {
            steps {
                // Execute Maven tests
                sh 'mvn clean test'
            }
        }

        stage('Publish Cucumber HTML Report') {
            steps {
                publishHTML([
                    reportDir: 'target',
                    reportFiles: 'cucumber-report.html',
                    reportName: 'Cucumber HTML Report',
                    keepAll: true,
                    alwaysLinkToLastBuild: true,
                    allowMissing: false
                ])
            }
        }

        stage('Publish Cucumber JSON Report') {
            steps {
                cucumber(
                    buildStatus: 'UNSTABLE',
                    fileIncludePattern: 'target/cucumber.json',
                    trendsLimit: 10
                )
            }
        }
    }

    post {
        always {
            // Publish JUnit test results
            junit 'target/surefire-reports/*.xml'
        }
    }
}
