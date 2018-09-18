
pipeline {
  agent {
    node {
      label 'master'
      def build_ok = true
    }
  }
  stages {
        stage('operate') {
          steps {
            script{
      
            sh '''
                  cd $TEST_REPO
                  cd 'sdfs
                  echo "operate" >> stage
                  
               '''
            
            }
           
          }
      }
    // some block
    stage('ok') {
      steps{
        
            sh '''
                  
                  echo "ok" >> $TEST_REPO/stage
                
               '''    
        
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
    STAGE_STATUS = 'default'
    BUILD_USER_EMAIL = 'shouchen.jiang@cloudiwz.cn'
    TEST_REPO = '/usr/local/auto-test'
    EMAIL_REPO = '/usr/local/auto-test/template'
    NEWMAN_REPO = '/usr/local/auto-test/newman'
    
  }
}
