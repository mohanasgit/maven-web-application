node{
    def mavenHome = tool name: "maven 3.8.1"
    properties([pipelineTriggers([pollSCM('* * * * *')])])
    stage('CheckoutCode'){
        git branch: 'development', credentialsId: '7cef8dd5-b079-4ba5-b1a3-b3578a3b01a8', url: 'https://github.com/mohanasgit/maven-web-application.git'
    }
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    /*stage('ExecuteSonarQubeReport'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('UploadArtifactIntoNexus'){
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('DeployAppIntoTomcat'){
     sshagent(['1c134a3a-6a08-4ca8-9d50-3fbcada538de']) {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.207.114.161:/opt/apache-tomcat-9.0.45/webapps/"
}   
    }
    */
    stage('EmailNotification'){
        emailext body: '''Build over and the status is sent

        Regards
        MohanaDevops''', subject: 'Build Status', to: 'mohana.manchala@gmail.com,krishnasreethan@gmail.com'
    }
}
