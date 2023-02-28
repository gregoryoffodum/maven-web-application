node{ 
    def mavenHome = tool name: "maven3.8.7"
	
try {
stage('CheckOutCode'){
    git branch: 'development', credentialsId: '0ed41650-be6d-461c-b525-be5f18b7db64', url: 'https://github.com/gregoryoffodum/maven-web-application.git'
}
stage('Build'){
    sh "${mavenHome}/bin/mvn clean package"
}
}
catch(e)
{
currentbuild.Result = 'FAILED'
throw e
}
finally{sendSlackNotifications(currentbuild.Result)}
}

def sendSlackNotifications(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    colorName = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    colorName = 'GREEN'
    colorCode = '#00FF00'
  } else {
    colorName = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}
