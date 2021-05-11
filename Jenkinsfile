pipeline {
    agent any
    environment {
        CI = 'true'
    }
    def changelogString = gitChangelog returnType: 'STRING'
    stages {
        stage('Build') {
            steps {
              echo changelogString 
            }
        }
        stage('Test') {
            steps {
               echo 'test' 
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
