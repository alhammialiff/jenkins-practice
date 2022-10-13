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
                    sh 'mvn clean package sonar:sonar'
                    
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