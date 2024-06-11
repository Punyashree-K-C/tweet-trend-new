pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.7/bin:$PATH"
}
    stages {
        stage("build"){
            steps {
                sh 'mvn clean deploy'
            }
        }
    stage('Build Docker Image') {
            steps {
                // Build the Docker image
                sh 'docker build -t ttrend-app:latest .'
            }
        }
        stage('Push Docker Image') {
            steps {
                // Login to Docker Hub (use Jenkins credentials)
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh 'echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin'
                }
                // Tag and push the Docker image
                sh 'docker tag ttrend-app:latest punya7899/ttrend-app:latest'
                sh 'docker push punya7899/ttrend-app:latest'
            }
        }


    }
}
        