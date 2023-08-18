node
{
    def mavenHome=tool name: "maven3.6.2"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5'))])
    
    stage('checkoutCode'){
        git branch: 'development', credentialsId: 'e4d0b5a4-47b2-4af1-a265-e6eca834b121', url: 'https://github.com/DevOpsFilesforPractice/maven-web-application.git'
    }
    stage('build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    /*stage('execute Sonar reports'){
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('upload artifact into artifactory repo'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }*/
    stage('deploy app to container'){
        sshagent(['31c13929-d5ae-4848-be73-4312c27ba3aa']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@43.205.213.227:/opt/apache-tomcat-9.0.79/webapps"
        }
    }
    /*stage('send a Email Notification'){
        mail bcc: 'khaleel.ka25@gmail.com', body: '''Build Over!!
        
        regards,
        khaleel''', cc: 'khaleel.ka2505@gmail.com', from: '', replyTo: '', subject: 'Build Over!!', to: 'khaleel.ka2534@gmail.com'
    }*/
    
    
}
