pipeline {
    agent any

    //environment {
    //    DOCKER_IMAGE = 'sahastra16/flask-app-new-web:latest'
    // }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/sahastra16/flask-app-new.git', branch: 'development'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t flask-app-new-web ."
                }
            }
        }
        stage('Run Containers') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
            }
        }
    
        stage("push to docker"){

            steps {

                 withCredentials([usernamePassword(

                    credentialsId:"dockerhub-creds",

                    passwordVariable: "dockerHubPass",

                    usernameVariable: "dockerHubUser"

                )]){

                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"

                sh "docker tag flask-app-new-web ${env.dockerHubUser}/flask-app-new-web"

                sh "docker push ${env.dockerHubUser}/flask-app-new-web:latest"

                }

            }

        }
        
    }
}    
