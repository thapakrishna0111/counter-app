pipeline{
  agent any
    stages{
      stage('git checkout'){
        steps{
           git branch: 'main', url: 'https://github.com/thapakrishna0111/counter-app.git'
        }
      }
      stage('UNIT Testing'){
        steps{
           sh 'mvn test'
        }
      }
     stage('Integration Testing'){
        steps{
           sh 'mvn verify -DskipUnitTests'
        }
      }
     stage('Maven Build'){
        steps{
           sh 'mvn clean install'
        }
      }
     stage('SonarQube Analysis'){
        steps{
           script {
             withSonarQubeEnv(credentialsId: 'sonar-auth') {
	     sh 'mvn clean package sonar:sonar'
	     }
           }
        }
      }
    stage('Quality Gate Status'){
        steps{
           script {
             waitForQualityGate abortPipeline: false, credentialsId: 'sonar-auth'
           }
        }
      }
    stage('Upload to Nexus'){
        steps{
           script {
             nexusArtifactUploader artifacts: 
               [
                 [
                   artifactId: 'springboot', 
                   classifier: '', 
                   file: 'target/uber.jar', 
                   type: 'jar'
                 ]
                ], 
                    credentialsId: 'Nexus-auth', 
                    groupId: 'com.example', 
                    nexusUrl: '192.168.1.8:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'demoapp-release', 
                    version: '1.0.1'
           }
        }
      }

    }

}
