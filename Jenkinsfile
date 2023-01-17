pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                snykSecurity( failOnError: false, failOnIssues: false, projectName: 'SynkTest', severity: 'medium', snykInstallation: 'InfoSec', snykTokenId: '66bed432-40d3-4182-83b9-6d988a6e05dc')
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo ./jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'sudo ./jenkins/scripts/kill.sh'
            }
        }
    }
}
