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
    stage('Build') {
      steps {
        container('maven') {
          script{
          final scmVars = checkout(scm)
            sh "echo scmVars: ${scmVars}"
          }
          sh 'mvn -version'
          sh 'env'
          sh "echo this is the url ${env.GIT_URL}"
          writeFile file: "application.sh", text: "echo Built ${BUILD_ID} of ${JOB_NAME}"
        archiveArtifacts artifacts: '*.sh', fingerprint: true
          
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
