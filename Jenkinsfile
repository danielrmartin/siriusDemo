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
            steps {
              script{
                if (env.BRANCH_NAME=="dev"){
               sh " echo Deploying"
                }
                else
                  sh "echo Not deploying"
              }
            }
        }
    stage ('Deploy to QA'){
     when {
                beforeAgent true
                branch 'master'
            }
            steps {
                echo 'Deploying'
            }
    }
    stage ('parent'){
     options {
    lock('myLock')
  }//end log
      stages {
    stage('first child') {
      steps{sleep 60}
    }//end first
    stage('second child') {
      steps { sleep 10}
    }//end second
  }//end parent
  }
}
