@Library('Jenkins-Library') _

pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'orisuniyanu/marketpeak'
        TAG = "${BUILD_NUMBER}-${env.GIT_COMMIT?.take(7)}"
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

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    deploK8s(DOCKER_IMAGE_NAME)
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
