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
        stage('Docker build Push Image'){
            steps {
                script {
                    docker.withRegistry('https://033407704869.dkr.ecr.us-west-2.amazonaws.com/bucketlist', 'ecr:us-west-2:aws-credentials') {
                        def customImage = docker.build("bucketlist:latest","./")
                        customImage.push()
                    }
                }
            }
        }
        stage('Deploy to EKS'){
            steps {
                 sh 'kubectl apply -f k8s'
            }
        }
    }
}