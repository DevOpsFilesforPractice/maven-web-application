node{
def mavenHome=tool name: "maven3.6.2"
stage('checkout code'){
git branch: 'stage', credentialsId: 'e4d0b5a4-47b2-4af1-a265-e6eca834b121', url: 'https://github.com/DevOpsFilesforPractice/maven-web-application.git'
}
stage('build'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('execute sonar reports'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('upload app into artifactory repo'){
sh "${mavenHome}/bin/mvn clean deploy"
}
stage('deploy app into container'){
sshagent(['31c13929-d5ae-4848-be73-4312c27ba3aa']) {
    sh "scp -o StrictHostKeyChecking=no /target/maven-web-application.war ec2-user@43.205.213.227:/opt/apache-tomcat-9.0.79/webapps
}
}
stage('email notification'){
mail bcc: 'khaleel.ka2534@gmail.com', body: '''thank you

regards
khaleel''', cc: 'khaleel.ka2534@gmail.com', from: '', replyTo: '', subject: 'build success!!', to: 'khaleel.ka2534@gmail.com'
}
}
