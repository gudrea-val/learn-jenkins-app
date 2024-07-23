pipeline {
    agent any

    stages {
 /*       stage ("Build") {
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
*/
        stage ("Test") {
            // Test stage
             agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                echo "Test stage"
                sh '''
                    test -f "build/index.html"
                npm test
                '''

            }
        }
         stage ("E2E") {
            // E2E Tests stage
             agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps{
                echo "E2E Test stage"
                sh '''
                    npm install -g serve
                    serve -s build
                    npx playwright test
                npm test
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