import com.acme.Build
def build=new Build(this)
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
          script{build.mvn("foo","bar","yo")}
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
  }
}
