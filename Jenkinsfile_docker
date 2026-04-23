pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                sh 'docker build -t my-first-image .'
            }
        }
        
        stage('Deploy/Test Run') {
            steps {
                echo "🚀 Deploying the container..."
                // This runs the container, shows the output, then deletes it (--rm)
                sh 'docker run --rm my-first-image'
            }
        }
    }
    
    post {
        success {
            echo "SUCCESS: The code was built into an image and successfully 'deployed'!"
        }
    }
}