pipeline {
    agent any 

    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/HGSChandeepa/test-node'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t dusantha638/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-password', variable: '123456789')]) {
                    bat "echo ${DOCKER_PASSWORD} | docker login -u dusantha638 --password-stdin"
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push dusantha638/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
