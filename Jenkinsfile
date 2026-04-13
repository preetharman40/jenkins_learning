pipeline {
    agent any
    
    environment {
        APP_NAME = "MyCoolApp"
        VERSION = "1.0.1" // Let's bump the version!
    }

    stages {

        stage('Logic Check') {
            steps {
                script {
                    // This is "Scripted" Groovy inside a Declarative Pipeline
                    def myName = "Senior DevOps Student"
                    def hour = 14 // Imagine it's 2 PM

                    if (hour < 12) {
                        echo "Good morning, ${myName}!"
                    } else {
                        echo "Good afternoon, ${myName}!"
                    }
                }
            }
        }
        stage('Build') {
            steps {
                echo "Building ${APP_NAME}..."
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                // Fun task: If you want to see a 'Failure', change 'true' to 'false' below
                sh 'true' 
            }
        }
    }

    // This is the new part!
    post {
        always {
            echo 'Cleaning up the workspace... (I always run)'
        }
        success {
            echo 'HOORAY! The build passed. Sending notification to the team...'
        }
        failure {
            echo 'OH NO! The build failed. Paging the DevOps engineer...'
        }
    }
}