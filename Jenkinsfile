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
                  
               '''
           
              }
             catch(Exception e){
           echo 'nothing'
       }
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

  
  environment {
    STAGE_STATUS = 'default'
    BUILD_USER_EMAIL = 'shouchen.jiang@cloudiwz.cn'
    TEST_REPO = '/usr/local/auto-test'
    EMAIL_REPO = '/usr/local/auto-test/template'
    NEWMAN_REPO = '/usr/local/auto-test/newman'
    
  }
}


