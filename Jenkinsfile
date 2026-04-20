pipeline {
    //pipeline eka run wena OS eka, AWS EC2 instance ekak wage ew that agent ekta danne.. methan any kiyla damma
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/FlorinNatha/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t Florin/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhubpass')]) {
                    script {
                        bat "docker login -u Florin -p %test-dockerhubpass%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push Florin/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}



