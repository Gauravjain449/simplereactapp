pipeline {
    agent any
  
    environment {
        PASSWORD = credentials('DOCKER_PASSWORD')
        REPOSITORY_TAG="${DOCKER_HUB_USER_NAME}/simple-app:${BUILD_ID}"
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
                sh 'docker build -t ${REPOSITORY_TAG} -f Dockerfile.dev .'
            }
        }

        stage('Docker image test') {
            steps {
                sh 'docker run -e CI=true ${REPOSITORY_TAG} npm run test'
            }
        }

        stage('Docker image push') {
            steps {
                sh 'echo "${PASSWORD}" | docker login -u "${DOCKER_HUB_USER_NAME}" --password-stdin'
                sh 'docker push ${REPOSITORY_TAG}'
            }
        }

        stage('kubernetes deployment') {
            steps {
                sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl delete -f -'
                sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
            }
        }
    }
}