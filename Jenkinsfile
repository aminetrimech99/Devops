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
                 sh 'docker build -t aminetr/springapp .'
            }
        }


       stage('login to DockerHub'){
            steps { 
		   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u aminetr -p amineamine'
                    
                }
       }
	       stage("Push to DockerHub") {
                steps{
                    sh 'docker push aminetr/springapp docker.io'
                }
        }
            
        
        stage('DockerCompose') {
        
                       steps {
                            
				            sh 'docker-compose up -d'
                        }
                          
        }
        }
    }

