pipeline {
    agent { label 'linux-prod' }

    stages {
        stage('Build & Test') {
            steps {
                echo "Building on Proxmox VM..."
                sh 'docker build -t my-app:${BUILD_NUMBER} .'
                sh 'docker run --rm my-app:${BUILD_NUMBER} echo "Tests Passed!"'
            }
        }
    }

    post {
        always {
            // 1. Clean the workspace files (Source code, logs, etc.)
            cleanWs()
            
            // 2. Clean up dangling Docker images to save disk space
            // The '|| true' ensures the build doesn't fail if there's nothing to prune
            sh 'docker image prune -f || true'
        }
        success {
            echo "✅ Build # ${BUILD_NUMBER} successful and environment cleaned."
        }
    }
}