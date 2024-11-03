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
                // Use withCredentials to access the Docker password
                withCredentials([string(credentialsId: '9437794b-ba13-4924-9197-314de82d653e', variable: 'DOCKER_PASSWORD')]) {
                    // Login to Docker Hub using the stored password
                    bat 'echo %DOCKER_PASSWORD% | docker login -u dusantha638 --password-stdin'
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
