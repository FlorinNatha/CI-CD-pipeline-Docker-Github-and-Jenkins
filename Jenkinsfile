pipeline {
    //pipeline eka run wena OS eka, AWS EC2 instance ekak wage ew that agent ekta danne.. methan any kiyla damma
    agent any 

    environment {
        IMAGE_NAME = "nathashaflorin/nodeapp-cuban"
    }
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/FlorinNatha/CI-CD-pipeline-Docker-Github-and-Jenkins.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhubpass')]) {
                    script {
                        bat "docker login -u nathashaflorin -p %test-dockerhubpass%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat "docker push %IMAGE_NAME%:%BUILD_NUMBER%"
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}



