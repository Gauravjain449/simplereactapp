pipeline {
    agent any

    stages {
        stage('Preparation'){
            steps {
                cleanWs()
                git credentialsId: 'GitHub', url: "https://github.com/Gauravjain449/simplereactapp.git"
            }
        }

        stage('Docker Hello World') {
            steps {
                sh 'docker run hello-world'
            }
        }
    }
}