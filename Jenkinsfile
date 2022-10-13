pipeline {
    agent { 
        node {
            label 'built-in-node'
            }
      }
    triggers {
        pollSCM '*/3 * * * *'
    }
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube Server'){
                    sh '''
                    sonar-scanner \
                    -Dsonar.projectKey=cynapseai-homework \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=sqp_d3ad9b95a547b0aa942e67f04859684cbbb73cfe
                    '''
                }
            }
        }
        stage('Build') {
            agent any
            steps {
                echo "Building.."
                sh '''
                cd src
                docker build -t test-app .
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                docker run test-app
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}