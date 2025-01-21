pipeline {
    agent any


    environment {
        NETLIFY_SITE_ID = 'b36d4dfb-8454-4070-ac17-808f6e8cec6e'
    }

    stages {
        stage("Build") {

            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage("Test") {
            steps {
                sh '''
               echo "Testing Stage"
                '''
            }
        }


        stage("Deploy") {

            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli

                    node_modules/.bin/netlify --version

                    echo "Deploying to PROD ID: $NETLIFY_SITE_ID"
                '''
            }
        }


        
    }
}