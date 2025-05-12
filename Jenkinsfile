@Library('Jenkins-Library-') _

pipeline {
    
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'marketpeak'
        TAG = "v${BUILD_NUMBER}"
    }

    stages {
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
    }
}
