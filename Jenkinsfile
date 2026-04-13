pipeline {
    agent any
    
    environment {
        APP_NAME = "MyCoolApp"
        VERSION = "1.0.2" // Let's bump the version!
    }

    stages {

        stage('Logic Check') {
            steps {
                script {
                    // This is "Scripted" Groovy inside a Declarative Pipeline
                    def myName = "Harman"
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
                echo "Building the project..."
            }
        }
        stage('Test') {
            steps {
                echo "Running unit tests..."
            }
        }
        stage('Deploy to Production') {
            // This stage will ONLY run if the branch is 'main'
            when {
                expression { 
                    return env.BRANCH_NAME == 'main' || env.GIT_BRANCH == 'origin/main' 
                }
            }
            steps {
                echo "🚀 DEPLOYING TO PRODUCTION! 🚀"
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