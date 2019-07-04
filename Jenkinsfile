pipeline {
  agent {
    node {
      label 'deploy'
    }
    
  }
  stages {
    stage('pull') {
      parallel {
        stage('pull permission master') {
          steps {
            sh '''cd $PERMISSION_REPO
                  source ~/.bash_profile
                  git checkout master
                  git checkout ${selected_branch#*/} || git checkout -b ${selected_branch#*/} "origin/"${selected_branch#*/}
                  git pull origin ${selected_branch#*/}
               '''
          }
        }
      }
    }
    stage('build permission-jar') {
      steps {
        sh '''cd $PERMISSION_REPO
              $M2_HOME/bin/mvn clean package
           '''
      }
    }
    stage('release file ') {
      steps {
        sh '''mkdir -p $RELEASES_DATA/$BUILD_NUMBER
              mv $PERMISSION_REPO/xxxxx.jar $RELEASES_DATA/$BUILD_NUMBER
              unlink /data/autodeploy/releases/permission/latest
              ln -s /data/autodeploy/releases/permission/$BUILD_NUMBER /data/autodeploy/releases/permission/latest
           '''
      }
    }
    stage(' note the build info to html ') {
      steps {
         wrap([$class: 'BuildUser']) {
            sh '''cd $PERMISSION_REPO
                   git pull origin ${selected_branch#*/}
                   branch=$(git branch | grep "*" |awk '{print $2}')
                   commit_id_long=$(git show |sed -n "1p" | awk '{print $2}')
                   commit_id=$(echo ${commit_id_long:0:6})
                   commit_description=$(git log -1 --pretty=%B | sed '/^$/d'|awk '{if(NR%2==0){printf $0 "\\n"}else{printf "%s：",$0}}')
                   build_description=$build_description
                   build_version=$BUILD_NUMBER
                   build_time=$(date -d today +"%Y-%m-%d-%H:%M")
                   sed -i "78i<p class='oneList'><span class='width100'>$build_version</span><span class='width150'>$build_time</span><span class='width150'>$commit_id</span><span class='width100'>$branch</span><span class='width400'>$commit_description</span><span class='width400'>$build_description</span><span class='width150'>$BUILD_USER</span></p>" /usr/share/nginx/html/jenkins/permission.html
                   cp -a /usr/share/nginx/html/jenkins/permission.html /usr/share/nginx/html/jenkins/html-history/permission-$build_time.html
                   git checkout master
                '''
         }
      }
    }
    stage('Test send email'){
      steps{
        echo 'Test email'
      }
      post {
success {
emailext (
subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
  to: "${BUILD_USER_EMAIL }",
body: """<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>第${BUILD_NUMBER}次构建日志</title>
</head>
 
<body leftmargin="8" marginwidth="0" topmargin="8" marginheight="4"
    offset="0">
    <table width="95%" cellpadding="0" cellspacing="0"
        style="font-size: 11pt; font-family: Tahoma, Arial, Helvetica, sans-serif">
        <tr>
            <td>
                <h2>
                    <font>Hi All, 以下是${PROJECT_NAME}项目在Jenkins异常情况邮件通知</br>
                             (本邮件是程序自动下发的，请勿回复！)</font>
                </h2>
            </td>
        </tr>
        <tr>
            <td>
                <br />
                <b><font color="#0B610B">构建信息</font></b>
               <hr size="2" width="100%" align="center" />
             </td>
        </tr>
        <tr>
            <td>
                <ul>
                    <li>项目名称 ： ${PROJECT_NAME}</li>
                    <li>构建编号 ： ${BUILD_NUMBER}</li>
                    <li>构建状态 ： success</li>
                    <li>触发原因 ：cause</li>
                    <li>构建日志 ： aaa</li>
                    <li>工作目录 ：bbbb</li>
                   
                </ul>
            </td>
        </tr>
 <tr>
            <td>
                <br />
                <b><font color="#0B610B">测试执行结果</font></b>
               <hr size="2" width="100%" align="center" />
              
                <tr>
            <td><b><font color="#0B610B">构建日志:</font></b>
            <hr size="2" width="100%" align="center" /></td>
        </tr>
        <tr>
            <td><textarea cols="140" rows="30" readonly="readonly"
                    style="font-family: Courier New">log</textarea>
            </td>
        </tr>
    </table>
</body>
</html>""",
recipientProviders: [[$class: 'DevelopersRecipientProvider']]
)
}
failure {
emailext (
subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
  to: "375479098@qq.com",
body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
<p>Check console output at "<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
recipientProviders: [[$class: 'DevelopersRecipientProvider']]
)
}
}
    }
  }
  environment {
    PERMISSION_REPO = ''
    JAVA_HOME = '/data/workspace/jdk1.8.0_121'
    M2_HOME = '/data/apache-maven-3.0.5'
    RELEASES_DATA = 'n'
    PROJECT_NAME = "Test"
  }
}
