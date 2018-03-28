pipeline {
  agent {
    node {
      label 'docker'
    }
    
  }
  stages {
    stage('build') {
      steps {
        sh 'echo mvn clean install'
      }
    }
    stage('deploy') {
      steps {
        sh 'echo ansible-cle playbook'
      }
    }
    stage('UI TEST') {
      parallel {
        stage('UI TEST') {
          steps {
            sh 'echo hello'
          }
        }
        stage('Firefox') {
          steps {
            sh 'echo foo'
          }
        }
        stage('Chrome') {
          steps {
            sh 'echo CHROME'
          }
        }
      }
    }
  }
}