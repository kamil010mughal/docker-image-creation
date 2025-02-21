pipeline {
    agent any

    environment {
        IMAGE_NAME = "kamil010mughal/docker-image-creation"  // Update with your GitHub package name
        GITHUB_USER = "kamil010mughal"  // Your GitHub username
        GITHUB_TOKEN = credentials('github-token')  // Use the correct credential ID
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    credentialsId: 'github-token',  // Added credentials ID
                    url: 'https://github.com/kamil010mughal/docker-image-creation.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Login to GitHub Container Registry') {
            steps {
                script {
                    sh 'echo $GITHUB_TOKEN | docker login ghcr.io -u $GITHUB_USER --password-stdin'
                }
            }
        }

        stage('Push Image to GitHub Packages') {
            steps {
                script {
                    sh 'docker tag $IMAGE_NAME ghcr.io/$IMAGE_NAME'
                    sh 'docker push ghcr.io/$IMAGE_NAME'
                }
            }
        }
    }
}
