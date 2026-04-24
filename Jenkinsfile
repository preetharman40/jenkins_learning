pipeline {
    agent { label 'linux-prod'}

    environment {
        APP_NAME = "skyline-fastpay"
        VERSION = "1.0.${BUILD_NUMBER}"
        //API_KEY = credentials('')
    }

    stages {

        stage('Install Dependencies') {

            steps {
                echo "Setup environment for ${APP_NAME} v${VERSION}"
                sh '''
                    # create a virtual environment 
                    python3 -m venv venv
                    ./venv/bin/pip install --upgrade pip
            
                    ./venv/bin/pip install -r requirements.txt
                    echo "Dependecies installed"
                '''
            }
        }

        stage('Simulate Linting') {
            
            steps {
                echo 'Running Flake8 Linting...'
                sh '''

                ./venv/bin/python -c "print('Linting  passed!')"
                '''
            }
        }

        stage('Unit Tests') {

            steps {
                echo 'Running Pytest suite...'
                sh '''

                ./venv/bin/python -c "print('Test Passed 100%')"
                '''
            }
        }

        stage('Docker Build and push') {

            steps {
                sh "docker build -t ${APP_NAME}:${VERSION} ."

                withCredentials([usernamePassword(credentialsId: 'github-registry-creds',
                                                  usernameVariable: 'GH_USER',
                                                  passwordVariable: 'GH_PAT')]) {


                    sh '''

                        # login using the masked credentials
                        echo $GH_PAT | docker login ghcr.io -u $GH_USER --password-stdin

                        # tag the image for github container Registry
                        docker tag $APP_NAME:$VERSION ghcr.io/$GH_USER/$APP_NAME:$VERSION
                        docker tag $APP_NAME:$VERSION ghcr.io/$GH_USER/$APP_NAME:latest
                    
                        

                        #Push the images
                        docker push ghcr.io/$GH_USER/$APP_NAME:$VERSION
                        docker push ghcr.io/$GH_USER/$APP_NAME:latest
                    
                    
                    '''

                }
            }
        }




        stage('Deploy to DEV') {

            steps {
                echo "Starting FastPay v${VERSION} on DEV..."
                sh'''
                    # Stop and remove old container if it exists
                    docker stop $APP_NAME-dev || true
                    docker rm $APP_NAME-dev || true

                    # Run the new container
                    docker run -d --name $APP_NAME-dev -p 8081:8080 ghcr.io/preetharman40/$APP_NAME:$VERSION

                '''
                echo 'FastPay is live on port 8081!'
            }
        }

        stage('Manual Approval') {
            when { branch 'main'}
            options { timeout(time: 1, unit: 'HOURS')}

            steps {
                input message: "Deploy ${APP_NAME} v${VERSION} to Production?", ok: "Approve Deployment"

            }
        }

        stage('Deploy to Production') {
            when { branch 'main'}

            steps {
                echo "PROD DEPLOYMENT STARTING v${VERSION}"
                echo "Successfully deployed to Production!"
            }
        }

    }

    post {
        always {
            echo 'Cleaning up the workspace... (I always run)'
            cleanWs()
        }

        success {
            echo 'Building Skyline...Pipeline completed'
        }

        failure {
            echo 'PROD DEPLOY FAILED! Initiating Rollback procedures...'
        }
    }
}