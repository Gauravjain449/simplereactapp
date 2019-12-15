pipeline {
    agent {
       docker {
            image 'node:alpine'
            args '-p 3000:3000'
        }
    }
    environment {
        CI= 'true'
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'npm run test'
            }
        } 
        stage('Create Build') {
            steps {
                sh 'npm run build'
            }
        } 
        
        stage('deploy') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                
            }
        } 

    }
}