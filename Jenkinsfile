pipeline {
    agent any


    environment {
        NETLIFY_SITE_ID = 'a9dab8fe-ff67-4784-b8fe-0af5e38b1a92'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
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

                    node_modules/.bin/netlify status

                    node_modules/.bin/netlify deploy --dir=build --prod
                '''
            }
        }


        
    }
}