pipeline {
    agent {
        label 'dev-agent'
    }
    
    stages{
        stage('Code'){
              steps {
                    git url: "https://github.com/mohdadnaanazam/node-todo-cicd", branch : 'master'
            }   
        }
        stage('Build and Test') {
              steps {
                  sh 'docker build . -t adnaanazam/node-todo-app-cicd:latest'
            }   
        }
        
        stage('Login and Push Image') {
            steps {
                  echo 'Logging in to docker hub and pushing image'
                  withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                      sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                      sh "docker push adnaanazam/node-todo-app-cicd:latest"
                  }
            }   
        }
              stage('Deploy'){
              steps {
                  sh 'docker-compose -p node-todo-app down && docker-compose -p node-todo-app up -d'
            }   
        }
        
    }
}
