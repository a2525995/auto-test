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
                  echo "opera1333311te22211114111" >> stage
                  echo "testttt"
                  echo 2999222
               '''
           
              }
             catch(Exception e){
              echo "12312334444"
       }
          }
      }
        }
    // some block
    stage('ok') {
      steps{
            
            
            sh '''
                  
                 echo "kk133223239972311231231232193338"
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


