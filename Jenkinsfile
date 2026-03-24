pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub-creds'  // Jenkins stored credentials ID
        DOCKER_HUB_USERNAME = 'akshay9480'
        BACKEND_IMAGE = "${DOCKER_HUB_USERNAME}/chat-backend:latest"
        FRONTEND_IMAGE = "${DOCKER_HUB_USERNAME}/chat-frontend:latest"
        KUBE_CONFIG_CREDENTIALS = 'kubeconfig-creds' // Jenkins stored kubeconfig ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/rajakumarck28/Real-Time-Chat-Application-Deployment-using-Kubernetes-CI-CD-Pipeline.git', branch: 'main'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('backend') {
                    script {
                        docker.build('chat-backend', '.')
                    }
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    script {
                        docker.build('chat-frontend', '.')
                    }
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS,
                                                  usernameVariable: 'DOCKER_USER',
                                                  passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                        sh "docker tag chat-backend ${BACKEND_IMAGE}"
                        sh "docker tag chat-frontend ${FRONTEND_IMAGE}"
                        sh "docker push ${BACKEND_IMAGE}"
                        sh "docker push ${FRONTEND_IMAGE}"
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: KUBE_CONFIG_CREDENTIALS, variable: 'KUBECONFIG_FILE')]) {
                    script {
                        sh 'mkdir -p $HOME/.kube'
                        sh 'cp $KUBECONFIG_FILE $HOME/.kube/config'
                        sh 'kubectl apply -f k8s/'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! 🎉'
        }
        failure {
            echo 'Deployment failed. ❌ Check logs!'
        }
    }
}
