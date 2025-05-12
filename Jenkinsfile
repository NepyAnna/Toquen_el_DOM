pipeline {
agent any

stages {
    stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${vitaflash}/${IMAGE_TD}:latest ."
                }
            }
        }

    stage('Tag Docker Image') {
            steps {
                script {
                    def sha = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                    env.IMAGE_TAG = sha
                    sh "docker tag ${vitaflash}/${IMAGE_TD}:latest ${vitaflash}/${IMAGE_TD}:${version001}"
                }
            }
        }

    stage('Push to DockerHub') {
        steps {
            script {
                sh "docker push ${IMAGE_TD}:${version001}"
            }
        }
    }

    }
  }
}
