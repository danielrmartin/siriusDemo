pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'mypod'
      containerTemplate {
        name 'maven'
        image 'maven:3.3.9-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Build maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
      }
    }
  }
}
