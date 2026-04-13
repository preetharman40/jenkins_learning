pipeline {
    agent any
    
    // This is like a global "Note to Self" for the pipeline
    environment {
        APP_NAME = "MyCoolApp"
        VERSION = "1.0.0"
    }

    stages {
        stage('Initialize') {
            steps {
                // We use ${} to use our variables inside the text
                echo "Starting the build for ${APP_NAME} version ${VERSION}"
            }
        }
        stage('Build') {
            steps {
                echo "Packaging ${APP_NAME}..."
            }
        }
    }
}