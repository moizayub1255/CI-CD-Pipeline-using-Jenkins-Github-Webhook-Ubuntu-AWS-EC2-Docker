pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "moizayub401@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/moizayub1255/CI-CD-Pipeline-using-Jenkins-Github-Webhook-Ubuntu-AWS-EC2-Docker.git'
            }
        }
    
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Docker Container Run') {
            steps {
                sh "docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }

        stage('Send Email Notification') {
            steps {
                emailext(
                    subject: "NestJS App Deployed Successfully on EC2!",
                    body: "Your Nest JS App is Deployed!\nhttp://54.159.65.176:3000/",
                    to: "${EMAIL}"
                )
            }
        }
    }
}