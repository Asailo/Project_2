@Library('your-shared-library') _

pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'marketpeak'  // Application name
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Call the shared library's build method
                    dockerBuild(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    // Call the shared library's push method
                    dockerPush(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Scan') {
            steps {
                script {
                    // Call the shared library's scan method
                    dockerScan(DOCKER_IMAGE_NAME)
                }
            }
        }
    }
}
