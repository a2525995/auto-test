pipeline {
  agent {
    node {
      label 'master'
    }
  }
  stages {
        stage('operate') {
          steps {1111
            script {
              try{
            sh '''
                  cd $TEST_REPO
                  dsfsdfsdfsfd
                  newman -c Auto-Test.json -e workspace.json -H test.html
                  echo "opera1333311te11114" >> stage
                  
               '''
           
              }
             catch(Exception e){
              echo "1231233"
       }
          }
      }
        }
    // some block
    stage('ok') {
      steps{
            
            
            sh '''exit 1
                  exit 0
                 echo "kk133223239972311231231232198"
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


