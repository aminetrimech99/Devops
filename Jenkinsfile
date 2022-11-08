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
                         artifactId: 'achat',
                         classifier: '',
                         file: 'target/achat-1.0.jar',
                         type: 'jar']], 
                     credentialsId: 'Devops',
                     groupId: 'tn.esprit.rh', 
                     nexusUrl: '192.168.1.26:8081', 
                     nexusVersion: 'nexus3', 
                     protocol: 'http',
                     repository: 'achat-realeases',
                     version: '1.0'
            }
              }
        stage('Docker image'){
            steps {
                 sh 'docker build -t amine/app .'
            }
        }


       stage('push image to DockerHub'){
            steps {
                  withCredentials([string(credentialsId: 'dockerHub-id', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u aminetr -p ${dockerhubpwd}'
                    sh 'docker push amine/app'
                }
            }
        }
        }
    }

