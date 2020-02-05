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
                sh 'docker build -t ${DOCKER_HUB_USER_NAME}/simple-app:${BUILD_ID} -f Dockerfile.dev .'
            }
        }
    }
}