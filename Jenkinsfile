pipeline{
   agent any
   
   stages{
      stage ('Git'){
        steps{
             git branch :'amine',
             url : 'https://github.com/aminetrimech99/Devops.git',
             credentialsId: 'git-token-token'
             
             }
       }
      stage ('MVN Clean')
       {
        steps{
               sh 'mvn clean install -DskipTests'
           }
       }
        stage ('MVN compile')
       {
        steps{
               sh 'mvn compile'
           }
       }
        stage ('build package')
       {
        steps{
               sh 'mvn clean package'
           }
       }

       stage('Docker image'){
           steps {
                sh 'docker build -t doukhou/springapp .'
           }
       }
       stage('DockerCompose') {
       
                      steps {
                           
                       sh 'docker-compose up -d'
                       }
                         
       }
      stage('push to DockerHub'){
           steps { 
        withCredentials([string(credentialsId: 'dockerHub1-id', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u doukhou -p ${dockerhubpwd}'
                   sh 'docker push doukhou/springapp'
                   
               }
      }
      }
        stage ('SonarQube :Quality Test')
       {
        steps{
            withSonarQubeEnv(installationName: 'sonar'){
               sh 'mvn sonar:sonar'
            }
           }
       }
      stage("Publish to Nexus Repository Manager") {
           steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'doukhou',
                        classifier: '',
                        file: 'target/doukhou-1.0.jar',
                        type: 'jar']], 
                    credentialsId: 'Devops',
                    groupId: 'tn.esprit.rh', 
                    nexusUrl: '192.168.1.12:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http',
                    repository: 'doukhou-realeases',
                    version: '1.0'
           }
             }
          
       
       
       }
   }
