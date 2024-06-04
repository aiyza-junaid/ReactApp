
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/aiyza-junaid/ReactApp.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                bat 'npm install' 
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t dockerr .'
            }
        }

        stage('Run Docker Image') {
            steps {
                bat 'docker run -d -p 3000:11 dockerr'
            }
        }

       
        }
}
