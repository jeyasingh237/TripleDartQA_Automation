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
    stage('Verify') {
      steps {
        sh 'pwd'
        sh 'ls -la'
      }
    }
  }
}
