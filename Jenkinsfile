pipeline {
agent any

stages {
    stage('Execute Command1') {
        steps {
            sh 'hostname'
            sh 'whoami'
        }
    }
    stage('Execute Command2') {
        steps {
            sh 'ls -ltra'
        }
    }
  }
}
