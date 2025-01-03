pipeline {
    agent any
    environment {
        IMAGE1 = 'app1'
        IMAGE2 = 'app2'
        TAG = "v1"
        DOCKER_USER = "mjid6"

    }
    stages {
        stage("clone the project"){
            steps {
                script {
                    branch "master", url ""
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    bat "docker build -t ${DOCKER_USER}/${IMAGE1}:${TAG} ./app1"
                    bat "docker build -t ${DOCKER_USER}/${IMAGE2}:${TAG} ./app2"
                }
            }
        }
        stage('Login to dockerhub') {
            steps {
                script {
                    bat "docker login -u mjid6 -p ${DOCKER_PASS}"
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    bat "docker push ${DOCKER_USER}/${IMAGE1}:${TAG}"
                    bat "docker push ${DOCKER_USER}/${IMAGE1}:${TAG}"
                    bat "docker images"
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    bat 'kubectl apply -f Kubernetes/app1-deployment.yaml --validate=false --kubeconfig=C:\\Users\\USER\\.kube\\config '
                    bat 'kubectl apply -f Kubernetes/app2-deployment.yaml --validate=false --kubeconfig=C:\\Users\\USER\\.kube\\config'
                }
            }
        }
    }
}

