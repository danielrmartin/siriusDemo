pipeline {
  agent {
    node {
      label 'larger'
    }
    
  }
  stages {
    stage('checkout') {
      steps {
        sh 'echo hello'
      }
    }
    stage('build') {
      steps {
        sh 'echo mvn clean install'
      }
    }
    stage('deploy') {
      steps {
        sh 'ansible-cle <playbook>'
      }
    }
    stage('UI TEST') {
      parallel {
        stage('UI TEST') {
          steps {
            sh 'hello'
          }
        }
        stage('Firefox') {
          steps {
            sh 'echo foo'
          }
        }
        stage('Chrome') {
          steps {
            sh 'ECHO CHROME'
          }
        }
      }
    }
  }
}