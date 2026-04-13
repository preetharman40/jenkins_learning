pipeline {
    agent any

    stages {
        stage('Debug Info') {
            steps {
                // This will tell us EXACTLY what Jenkins sees
                echo "DEBUG: The branch name according to Jenkins is: ${env.BRANCH_NAME}"
                echo "DEBUG: The GIT branch is: ${env.GIT_BRANCH}"
            }
        }
        stage('Build') {
            steps {
                echo "Building..."
            }
        }
        stage('Deploy') {
            // Let's use a more 'flexible' check for now
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
}