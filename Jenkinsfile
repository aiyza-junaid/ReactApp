pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials') 
        DOCKER_IMAGE = 'aiyzajunaid/simple-reactjs-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aiyza-junaid/ReactApp.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                bat 'npm install' 
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    dockerImage.run('-p 5000:5000')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
