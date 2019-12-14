pipeline {
    agent {
        label 'node-10.15.3'
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
         stage('Run Application') {
            steps {
                sh 'npm start'
            }
        } 

    }
}