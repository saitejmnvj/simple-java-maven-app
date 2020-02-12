pipeline {
    agent any
    tools {
        maven "maven"   
    }    
    stages {
       /*stage('Build stage') {
            steps {
                sh 'mvn clean package'
            }
        }*/
        stage("Sonar Code Analysis"){
            steps{
               withSonarQubeEnv('sonar'){
                    sh 'mvn sonar:sonar'
                    //org.codehaus.mojo:sonar-maven-plugin::sonar can alternatively used for sonar:sonar
                }
            }
        }
        stage('nexus upload'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: '/var/lib/jenkins/workspace/sample1/target/my-app-1.0-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'com.mycompany.app', nexusUrl: '127.0.0.1:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'samplerepo', version: '1.0-jenkins'      
            }
        }
     
    }
}
