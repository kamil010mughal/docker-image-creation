pipeline {
    agent any

    environment {
        IMAGE_NAME = "OWNER/REPO_NAME"   // Change to your GitHub package name
        GITHUB_USER = "your-github-username"
        GITHUB_TOKEN = credentials('github-token')  // Store GitHub token in Jenkins credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
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
