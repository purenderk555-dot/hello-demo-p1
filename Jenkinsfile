pipeline {
    agent any

    environment {
        DOCKER_HOST = "unix:///var/run/docker.sock"
    }

    stages {

        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/purenderk555-dot/hello-demo-p1.git', branch: 'main'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                eval $(minikube -p minikube docker-env)
                docker build -t hello-demo:v1 .
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }

    }
}

