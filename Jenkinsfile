pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *')
    }
    stages {
        stage('Build') {
         steps {
             sh './build.sh'

         }
         post{
            always{
                junit 'build/test-results/test/*.xml'
            }
         }

        }
        stage('Deploy') {
          steps {
              sh './deploy.sh'
          }
        }
        stage('Verify') {
           steps {
               sh './verify.sh'
           }
           post{
               always{

                   junit 'build/test-results/verify/*.xml'
               }
           }
        }

    }
    post {
        success {
            echo 'El job finalizó OK! :)'
        }
        failure {
            echo 'El job rompio! :('
        }
    }
}