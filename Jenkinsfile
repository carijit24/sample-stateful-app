pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'No Build required'
            }
        }
        stage('Unit Test'){
            steps {
                 echo 'No unit test '
            }
        }
        stage('Docker build'){
            steps{
                script {
                  docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push Image'){
            steps {
                script {
                    docker.withRegistry('https://033407704869.dkr.ecr.us-west-2.amazonaws.com/testrepo', 'ecr:us-west-2:aws-credentials') {
                        def customImage = docker.build("bucketlist:v${env.BUILD_NUMBER}","./")
                        customImage.push()
                        customImage.push("latest")
                    }
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