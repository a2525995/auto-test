
pipeline {
  agent {
    node {
      label 'master'
    }
  }
  stages {
    stage('pull') {

        stage('operate') {
          steps {
            sh '''
                  cd $TEST_REPO
                  newman -c Auto-Test.json -e workspace.json -H test.html
               '''
          }
      }
    }
  }
 //Send Email   
   post{
     //SUCCESS
        success{
            script { 
                wrap([$class: 'BuildUser']) {
                  sh ''' cd ${EMAIL_REPO}
                         ./send_email.sh ${BUILD_USER_EMAIL} SUCCESS ${JOB_NAME} ${BUILD_NUMBER} ${BUILD_URL} ${NEWMAN_REPO}
                     '''
                }
            }
        }
     
//FAILURE
        failure{
            script { 
                wrap([$class: 'BuildUser']) {
                sh ''' cd ${EMAIL_REPO}
                         ./send_email.sh ${BUILD_USER_EMAIL} FAILURE ${JOB_NAME} ${BUILD_NUMBER} ${BUILD_URL} ${NEWMAN_REPO}
                     '''
                }
            }
        }
}
     
  
  environment {
    TEST_REPO = '/usr/local/auto-test'
    EMAIL_REPO = '/usr/local/auto-test/template'
    NEWMAN_REPO = '/usr/local/auto-test/newman'
    
  }
}
