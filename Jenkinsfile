pipeline {
    agent any

    stages {
        stage('Docker Version Check') {
            steps {
                // Let's see if Jenkins can talk to Docker
                sh 'docker --version'
            }
        }
        stage('Build Docker Image') {
            steps {
                // This builds an image named 'my-first-image' using the Dockerfile in the current folder (.)
                sh 'docker build -t my-first-image .'
                echo "Docker Image Built Successfully!"
            }
        }
    }
}