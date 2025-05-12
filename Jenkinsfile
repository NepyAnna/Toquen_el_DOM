pipeline {
    agent any

    environment {
        IMAGE_NAME = 'image_toquen_el_dom'                      // Variable to store your app name
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds'              // Jenkins credential ID
        DOCKER_USER = 'vitaflash'            
        IMAGE_TAG = 'version_first'                           // Variable to store the image tag
    }

    stages {
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "${DOCKER_CREDENTIALS_ID}",
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${env.DOCKER_USER}/${env.IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    def sha = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
                    env.IMAGE_TAG = sha
                    sh "docker tag ${DOCKER_USER}/${IMAGE_NAME}:latest ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${DOCKER_USER}/${IMAGE_NAME}:latest"
                    sh "docker push ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}


