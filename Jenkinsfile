node
{
    def mavenHome= tool name : "Maven-3.8.6"
    
    stage('ramisdoingcheckoutfromthegithub')
    {
        git branch: 'development', credentialsId: '0c42bf7b-b7c9-4213-a7e5-f5df4b7870f1', url: 'https://github.com/Poojitha1305/maven-web-application.git'
    }
    
    stage("doingbuild")
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonarQubeReport')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage('Uploadartifcatsintoartifcatory')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    
    stage('DeplopytoTomcatServer')
    {
        sshagent(['bcaf2e0b-944b-4660-aeb9-00d5cdcbe739'])
        {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@34.227.56.177:/opt/apache-tomcat-9.0.64/webapps/"
        }
        
    }
    
}
