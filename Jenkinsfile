
properties([parameters([choice(choices: 'master\nesafe', description: 'Select Branch to build', name: 'branch')])])

node{
    stage('Scm Checkout'){
        echo "Pulling changes from the branch ${params.branch}"
        git url: 'https://github.com/seenuvasu145/multibranch-pipeline', branch: "${params.branch}"
    }
    
}
node{
    stage('SCM Checkout'){
         git 'https://github.com/seenuvasu145/my-app.git'
}
    stage('Compile-Package'){

         def mvnHome = tool name: 'maven-3', type: 'maven' 
         sh "${mvnHome}/bin/mvn package"
} 
     stage('Slack Notification'){
           slackSend baseUrl: 'https://hooks.slack.com/services/', 
           channel: 'jenkins-pipeline', color: 'good', 
           message:"${currentBuild.result}: ${BUILD_URL} ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}", 
           teamDomain: 'esafe build notification', 
           tokenCredentialId: 'slack-notification',
           body: '${currentBuild.result}: ${BUILD_URL}',
           subject: 'Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}'

}

    stage('Attachment Log'){
          emailext attachLog: true, body: '${currentBuild.result}: ${BUILD_URL}', 
          compressLog: true, replyTo: 'mohamed.sadiqh@gmail.com', 
          subject: 'Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}', to: 'vasucena145@gmail.com'
}

}
