pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'b1', url: 'https://github.com/DarshikaSahu/jenkins-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t ml_project:1.0 .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat 'docker run -d --name ml_app_container ml_project:1.0'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                        bat 'docker tag ml_project:1.0 darshikasahu/ml_project:1.0'
                        bat 'docker push darshikasahu/ml_project:1.0'
                    }
                }
            }
        }
    }
}
