pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'your_dockerhub_username'
        DOCKERHUB_PASS = credentials('dockerhub-pass')
        IMAGE_NAME = 'your_dockerhub_username/calculator'
    }

    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/your-username/ci-cd-calculator.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}
