pipeline {
    agent any
    stages {
        stage('ContinuousDownload') {
            steps {
                 git 'https://github.com/pavankumarindian/java-app.git'
            }
        }

        stage('ContinuousBuild') {
            steps {
                sh 'mvn package'
            }
        }

        stage('ContinuousDeployment') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'e595a2f2-e10e-4ee9-86f6-aed9abb38ee5', path: '', url: 'http://10.0.0.36:8080')], contextPath: 'qascriptedpipeline', war: '**/*.war'
            }
        }

        stage('ContinuousTesting') {
            steps {
                git branch: 'main', url: 'https://github.com/pavankumarindian/testing.git'
                sh 'java -jar /var/lib/jenkins/workspace/scripted-pipeline/testing.jar'
            }
        
        }

        stage('ContinuousDelivery') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '878b3733-5cd3-45ff-a602-e68f50d81511', path: '', url: 'http://10.0.0.171:8080')], contextPath: 'prodscriptedpipeline', war: '**/*.war'
            }
        
    }

    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
    
}
