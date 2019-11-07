pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
  }
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
    stage('Build') {
      steps {
        container('maven') {
          script{
          final scmVars = checkout(scm)
            sh "echo scmVars: ${scmVars}"
          }
          //sh 'mvn -version'
          writeFile file: "application.sh", text: "echo Built ${BUILD_ID} of ${JOB_NAME}"
         //gateProducesArtifact file: 'application.sh', label: 'application.sh:${BUILD_ID}'
          
        }
      }
    }  
     stage('Deploy') {
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
              publishEvent simpleEvent('helloWorld')
            }
    }
  }
}
