pipeline {
    agent any
    tools {
        maven "Maven"   
    }    
    stages {
        stage('Build stage') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Sonar Code Analysis"){
            steps{
               withSonarQubeEnv('sonar'){
                    sh 'mvn sonar:sonar -Pprofile1'
                    //org.codehaus.mojo:sonar-maven-plugin::sonar can alternatively used for sonar:sonar
                }
            }
        }
        stage('nexus upload'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'hexagon', classifier: '', file: '/var/lib/jenkins/workspace/SonarQube/target/hexagon-1.0-Hexagon.jar', type: 'jar']], credentialsId: '44c0662e-9030-4882-8aa3-b804b1a41316', groupId: 'hexagon6', nexusUrl: '18.224.155.110:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'devopstraining', version: '1.0-Hexagon'      
            }
        }
     
    }
}
