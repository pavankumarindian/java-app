node('')
{
    stage('ContinuesDownload')
    {
        git 'https://github.com/techcorporatetrainigs/java-app.git'
    }
    stage('ContinuesBuild')
    {
        sh 'mvn package'
    }
    stage('ContinuesDeployment')
    {
        deploy adapters: [tomcat9(credentialsId: '53dfb1c2-1e56-4a48-96c9-af1349300678', path: '', url: 'http://172.31.14.102:8080')], contextPath: 'qapipeline', war: '**/*.war'
    }
    stage('ContinuesTesting')
    {
        git branch: 'main', url: 'https://github.com/techcorporatetrainigs/testing.git'
        sh 'java -jar /var/lib/jenkins/workspace/dev-java-app/testing.jar'
    }
    stage('ContinuesDelivery')
    {
        deploy adapters: [tomcat9(credentialsId: '44bf5732-1878-448a-8497-18cfdbdee6b7', path: '', url: 'http://172.31.15.56:8080')], contextPath: 'prodpipeline', war: '**/*.war'
    }
}
