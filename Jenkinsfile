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
    stage('Verify maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
          sh 'env'
        }
      }
    }  
     stage('Example Deploy') {
            when {
                branch 'dev'
            }
            steps {
                echo 'Deploying'
            }
        }
    stage ('Deploy to QA'){
      steps{
        echo 'deploying to qa'
      }
  }
}
