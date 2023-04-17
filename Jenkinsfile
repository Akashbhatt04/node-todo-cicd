pipeline {
    agent {label 'dev-agent'}

    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/Akashbhatt04/node-todo-cicd.git', branch:'master'
            }
        }
        stage('buid and testing') {
            steps {
                sh 'docker build . -t aakashbhatt04/node-todo-app-cicd:latest'
            }
        }
        stage('Login and push Image') {
            steps {
                echo 'Logging into docker hub and pushing image'
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubpassword', usernameVariable:'dockerhubuser')]){
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpassword}"
                    sh "docker push aakashbhatt04/node-todo-app-cicd:latest"
                }    
            }
        }
        stage('deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
