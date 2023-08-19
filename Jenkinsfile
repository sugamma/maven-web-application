node 
{
    def mavenHome = tool name: "MavenHome"
    stage ('checkoutcode')
    {
        git credentialsId: 'e79f28c3-1902-4f7b-bcf5-87a4d2003aa7', url: 'https://github.com/sugamma/maven-web-application.git'
    }
    stage ('Build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    /*
    stage ('excutesonarquebereport')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    */
    stage ('uploadartifactnexus')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage ('Deployee to container')
    {
        deploy adapters: [tomcat9(credentialsId: '2e0f886f-b80f-425b-bd00-c535ac5caf68', path: '', url: 'http://192.168.225.244:9845/')], contextPath: null, war: '**/maven-web-application.war'
    }
    stage ('send email')
    {
        emailext body: '''Thanks,
Siddu''', subject: 'BUILD succcess', to: 'siddalingaswami11@gmail.com'
    }
}
