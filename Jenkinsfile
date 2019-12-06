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
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            steps {
                script{
            branch = "${env.BRANCH_NAME}" 
                sh (script:"/var/lib/jenkins/scripts/./deploy-test-web ${env.BRANCH_NAME}")
                }
      
            }
        }
    }
}
