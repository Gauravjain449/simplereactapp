pipeline {
    agent any
    environment {
       registryCredential = 'DOCKER_PASSWORD'
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
                sh 'docker build -t ${DOCKER_HUB_USER_NAME}/simple-app:${BUILD_ID} -f Dockerfile.dev .'
            }
        }

         stage('Docker image test') {
            steps {
                sh 'docker run -e CI=true ${DOCKER_HUB_USER_NAME}/simple-app:${BUILD_ID} npm run test'
            }
        }

         stage('Docker image push') {
            steps {
                sh "docker login -u ${DOCKER_HUB_USER_NAME} -p $registryCredential"
                sh 'docker push ${DOCKER_HUB_USER_NAME}/simple-app:${BUILD_ID}'
            }
        }
    }
}