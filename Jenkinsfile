pipeline {
    agent any

    stages {
        stage('Preparation'){
            steps {
                cleanWs()
                git credentialsId: 'GitHub', url: "https://github.com/Gauravjain449/simplereactapp.git"
            }
        }

        stage('Docker build image') {
            steps {
                sh 'docker build -t gauravjain449/simple-app -f Dockerfile.dev .'
            }
        }
    }
}