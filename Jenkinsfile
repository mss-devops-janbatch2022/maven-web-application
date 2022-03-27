node{

def mavenHome = tool name: "maven3.8.4"

//CheckOut Stage
stage("CheckOut Code"){
git branch: 'development', credentialsId: '797700ad-44ac-4cfc-b16f-dc066c07a631', url: 'https://github.com/mss-devops-janbatch2022/maven-web-application.git'
}

//Build Stage
stage("Build"){
sh "$mavenHome/bin/mvn clean package"
}

//Generate SonarQube Report
stage("SonarQubeReport"){
sh "$mavenHome/bin/mvn sonar:sonar"
}

//Upload Artifact Into Artifactory Repo
stage("Upload Artifactory"){
sh "$mavenHome/bin/mvn deploy"
}
//Deploy App into Tomcat Server
stage("DeployIntoTomcat"){
sshagent(['515aaa45-c101-4857-97cd-6c32f7850313']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.142.219:/opt/apache-tomcat-9.0.59/webapps"
}
}

}// node closing
