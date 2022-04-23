node{
    
def mavenHome = tool name: "maven3.8.4"

//Checkout Stage
stage('CheckoutCode'){

git branch: 'development', credentialsId: '090b06a1-95ab-40e5-b3e5-23bcda9f2ca1', url:
 'https://github.com/mss-devops-janbatch2022/maven-web-application.git'

}
//Build Stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//SonarQube Report
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn sonar:sonar"
}

//Upload Artifact into Artifcatory Repo
stage('NexusArtifcatoryRepo'){
sh "$mavenHome/bin/mvn deploy"
}

//Deploy App into Tomcat server
stage('DeployAppIntoTomcat'){
sshagent(['1881126d-2829-4496-a3ec-446ea26dd440']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.104.141:/opt/apache-tomcat-9.0.62/webapps"

}

}


}//Node Closing
