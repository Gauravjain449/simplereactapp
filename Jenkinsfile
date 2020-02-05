pipeline {
    agent any
  
    environment {
    registry = "gauravjain449/simple-app"
    registryCredential = 'DOCKER_PASSWORD'
    dockerImage = ''
    }

    stages {
        stage('Preparation'){
            steps {
                cleanWs()
                git credentialsId: 'GitHub', url: "https://github.com/Gauravjain449/simplereactapp.git"
            }
        }

        stage('Docker build image') {
            steps {
                script {
                dockerImage = docker.build  registry + ':${BUILD_ID} -f Dockerfile.dev .'
                }
            }
        }

         stage('Docker image test') {
            steps {
                sh 'docker run -e CI=true ${DOCKER_HUB_USER_NAME}/simple-app:${BUILD_ID} npm run test'
            }
        }

         stage('Docker image push') {
            steps {
                 script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }
                }
            }
        }
    }
}