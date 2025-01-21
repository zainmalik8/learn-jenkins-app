pipeline {
    agent any

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
                    npm install netlify-cli -g

                    netlify --version
                '''
            }
        }


        
    }
}