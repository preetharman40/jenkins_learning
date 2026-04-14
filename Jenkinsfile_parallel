// this has parallel LANE

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the app..."
            }
        }
        
        // This is the magic part
        stage('Run All Tests') {
            parallel {
                stage('UI Tests') {
                    steps {
                        echo "Starting UI Tests..."
                        sh 'sleep 5' // Simulates a 5-second task
                        echo "UI Tests Finished!"
                    }
                }
                stage('API Tests') {
                    steps {
                        echo "Starting API Tests..."
                        sh 'sleep 5'
                        echo "API Tests Finished!"
                    }
                }
                stage('Security Scan') {
                    steps {
                        echo "Starting Security Scan..."
                        sh 'sleep 5'
                        echo "Security Scan Finished!"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying after all parallel tasks succeeded!"
            }
        }
    }
}