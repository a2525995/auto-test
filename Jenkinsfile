
pipeline {
  agent {
    node {
      label 'master'
    }
  }
  stages {
        stage('operate') {
          steps {
            script {
              try{
            sh '''
                  cd $TEST_REPO
                  newman -c Auto-Test.json -e workspace.json -H test.html
                  echo "operate" >> stage
                  echo "kk"
                  
               '''
           
              }
             catch(Exception e){
          
       }
          }
      }
    // some block
    stage('ok') {
      steps{
            
            
            sh '''
                  
                  
                 currentBuild.result = 'SUCCESS'
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
