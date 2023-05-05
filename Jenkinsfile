pipeline {
    agent { label 'dev-agent' }
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/Ashishraj99/to-do-list-cloud/node-todo-cicd.git', branch: 'main'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build . -t Ashishraj/node-todo-app-cicd:latest' 
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'logging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push Ashishraj/node-todo-app-cicd:latest"
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
