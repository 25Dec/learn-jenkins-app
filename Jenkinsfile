pipeline {
    agent any

    environment {
        SITE_ID = 'oX912312-aq232jsad-123123'
        NODE_VERSION = 'node:18-alpine'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image "${NODE_VERSION}"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm ci
                    npm run build
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image "${NODE_VERSION}"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm i netlify-cli
                    node_modules/.bin/netlify
                    echo "Deploy to Site ID: $SITE_ID"
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}