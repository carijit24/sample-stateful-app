pipeline {
    agent none
    environment {
      registry = "033407704869.dkr.ecr.us-west-2.amazonaws.com/testrepo"
      registryCredential = ‘aws-credentials’
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile hello.py'
                stash(name: 'compiled-results', includes: '*.py*')
            }
        }
        stage('Unit Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Docker build'){
            script {
              docker.build registry + ":$BUILD_NUMBER"
            }
        }
        stage('Push Image'){
            steps {
                script {
                  docker.withRegistry( '', registryCredential ) {
                  dockerImage.push()
                }
            }
        }
        stage('Deploy to EKS'){
            steps{
                echo 'Deploy to EKS'
            }
        }
    }
}