node {
    try {
        stage('Stage Checkout') {
            checkout scm
            echo "My branch is: ${env.BRANCH_NAME}"
        }
        stage('Stage Build') {
            sh "mvn clean deploy -Dmaven.test.skip=true -U"
        }
        stage('Stage Builddiscard') {
            properties([[$class: 'GitLabConnectionProperty', gitLabConnection: 'gitlab'], buildDiscarder(logRotator(daysToKeepStr: '3', numToKeepStr: '3'))])
        }
    }
    catch (err) {
        currentBuild.result = "FAILED"
       // sh "sed -i 's!env.BUILD_URL!${env.BUILD_URL}!g' dingding.json"
      //  sh "sed -i 's!env.JOB_NAME!${env.JOB_NAME}!g' dingding.json"
       // sh "curl -X POST https://oapi.dingtalk.com/robot/send?access_token=ae3b70e881246f10b2302a471209b258cfc3dc3faa57bef05215f8ad9c226a70 -d @dingding.json -H 'Content-type:application/json'"
        throw err
    }


}




