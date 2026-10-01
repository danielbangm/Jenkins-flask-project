pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/danielbangm/Jenkins-flask-project.git',
                    branch: 'dman/jenkins-project'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t YOUR_DOCKERHUB_USERNAME/flask-app .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        passwordVariable: 'DOCKER_PASSWORD',
                        usernameVariable: 'DOCKER_USERNAME'
                    )
                ]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker push YOUR_DOCKERHUB_USERNAME/flask-app'
                }
            }
        }
    }
}