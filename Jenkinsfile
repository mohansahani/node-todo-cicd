pipeline {
    agent { label 'dev-agent' }
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/mohansahani/node-todo-cicd.git', branch: 'master'
            }
        }
        
        stage('Build and Test'){
            steps {
                sh 'docker build . -t mohansahani/node-todo-app:latest' 
            }
        }
        
        stage('Login and Push Image'){
            steps {
                echo 'Login into docker hub and pushing the image'
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUsername')]){
                sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"
                sh "docker push mohansahani/node-todo-app:latest"
                }
            }
        }
        
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        
    }
}
