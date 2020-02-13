pipeline {
    agent any
    tools {
        maven "maven"   
    }    
    stages {
       stage('Build stage') {
            steps {
                sh 'mvn clean package'
            }
        }
        /*stage("Sonar Code Analysis"){
            steps{
               withSonarQubeEnv('sonar'){
                    sh 'mvn sonar:sonar'
                    //org.codehaus.mojo:sonar-maven-plugin::sonar can alternatively used for sonar:sonar
                }
            }
        }*/
        stage('nexus upload'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: '/var/lib/jenkins/workspace/CI/target/my-app-1.0.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'com.mycompany.app', nexusUrl: '13.59.91.242:8081/nexu', nexusVersion: 'nexus2', protocol: 'http', repository: 'Devops', version: '2.0-SNAPSHOT'
            }
        }
     
    }
}
