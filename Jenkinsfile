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
    options {
        timeout(time: 1, unit: 'HOURS')
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
        stage('Create Builds') {
           parallel {
               stage('Build DEV') {
                   agent {
                       docker {
                           image 'node:alpine'
                       }
                   }
                   when {
                       beforeAgent true
                       branch 'master'
                   }
                   steps {
                       sh 'npm install'
                       sh 'npm run build'
                   }
                }
                stage('Build Staging') {
                    agent {
                        docker {
                            image 'node:alpine'
                        }
                    }
                    when {
                        beforeAgent true
                        branch 'master'
                    }
                    steps {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
           
            }
        }

    }
}