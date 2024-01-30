pipeline {
    agent { label 'dev' }
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/mohansahani/node-todo-cicd.git', branch: 'master'
            }
        }
        
        stage('Buils and Test'){
            steps {
                sh 'docker build . -t mohansahani/node-todo-app-new:latest'
            }
        }
        
        stage('Login and Push Image'){
            steps {
                echo 'Login to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push mohansahani/node-todo-app-new:latest"
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
