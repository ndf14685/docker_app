#This Jenkinsfile is used by Jenkins to run the pipeline for this application.
pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "ndf14685/docker_app"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t homer-page 00-homer_page/'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'docker run --name homer-page --network jenkins -d --publish 8081:80 homer-page:1.0.0-1'
            }
        }
        stage('Registry') {
            steps {
                echo 'Pushing to registry..'
                sh 'docker tag homer-page:latest
                    homer-page:latest'
                sh 'docker push homer-page:latest'
            }
        }
#        stage('Kubernetes config pod') {
#            steps {
###                echo 'Install pod on Kubernetes..'
#                sh 'kubectl apply -f 00-homer_page/01-pod/pod.yaml'
#                echo 'Open port-fordwarding..'
#                sh 'sh 01-pod/port-forward.sh'
#            }

#        }
#        stage('Kubernetes deploy pod') {
#            steps {
#                echo 'Config Kubernetes deployment..'
#                sh 'kubectl apply -f 00-homer_page/02-deployment/deployment.yml'
#                echo 'Config Kubernetes service..'
#                sh 'kubectl apply -f 00-homer_page/02-deployment/service.yml'
#            }
#        }
        

    }
    post {
        always {
            echo 'Cleaning up..'
            sh 'docker stop homer-page'
            sh 'docker rm homer-page'
        }
    }
}

