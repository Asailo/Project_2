@Library('Jenkins-Library') _

pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'orisuniyanu/marketpeak'
        TAG = "v${BUILD_NUMBER}"
        KUBECONFIG = "${WORKSPACE}/admin.conf"
    }

    stages {
        stage('Debug') {
            steps {
                echo "TAG: ${TAG}"
                echo "DOCKER_IMAGE_NAME: ${DOCKER_IMAGE_NAME}"
            }
        }

        stage('Build') {
            steps {
                script {
                    build(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Scan') {
            steps {
                script {
                    scan(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    push(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Deploy to Prod VM') {
            steps {
                script {
                    deploy(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                        cp $KUBECONFIG_FILE $KUBECONFIG
                        kubectl apply -f k8s/deployment.yaml
                        kubectl apply -f k8s/service.yaml
                    '''
                }
            }
        }

        stage('Clean Unuse Container and Image') {
            steps {
                script {
                    clean(DOCKER_IMAGE_NAME)
                }
            }
        }
    }
}
