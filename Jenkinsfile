pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node'
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

        stage('Test') {
            agent {
                docker {
                    image 'node'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-result/junit.xml'
        }
    }
}