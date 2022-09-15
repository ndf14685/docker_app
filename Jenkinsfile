#This Jenkinsfile is used by Jenkins to run the pipeline for this application.
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t docker_app .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'docker run docker_app'
            }
        }
        stage('Registry') {
            steps {
                echo 'Pushing to registry..'
                sh 'docker tag docker_app:latest
                    docker_app:latest'
                sh 'docker push docker_app:latest'
            }
        }
    }
}