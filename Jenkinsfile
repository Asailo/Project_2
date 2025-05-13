@Library('Jenkins-Library') _

pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'orisuniyanu/marketpeak'
        TAG = "v${BUILD_NUMBER}"
    }

    stages {
        stage('Debug') {
            steps {
                echo "TAG: ${TAG}" // Debug the tag value
                echo "DOCKER_IMAGE_NAME: ${DOCKER_IMAGE_NAME}" // Debug the image name
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
    }
}
