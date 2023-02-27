node{ 
    def mavenHome = tool name: "maven3.8.7"
stage('CheckOutCode'){
    git branch: 'development', credentialsId: '0ed41650-be6d-461c-b525-be5f18b7db64', url: 'https://github.com/gregoryoffodum/maven-web-application.git'
}
stage('Build'){
    sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('ExecuteSonarQubeReport'){sh "${mavenHome}/bin/mvn sonar:sonar"}

stage('UploadArtifactIntoNexus'){sh "${mavenHome}/bin/mvn clean deploy"}

stage('DeployAppIntoTomcatServer'){sshagent(['8dfdc3e9-1580-4638-abf3-63b233a36743']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.87.130:/opt/apache-tomcat-9.0.71/webapps"
}
    
}
*/
}
