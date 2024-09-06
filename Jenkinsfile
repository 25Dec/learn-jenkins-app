pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = "oX912312-aq232jsad-123123"
        NETLIFY_TOKEN = credentials('netlify-token')
        NODE_VERSION = "node:18-alpine"
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
                    node_modules/.bin/netlify login
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