pipeline {
    agent any
    environment { 
        registry = "farouk973/springdevops" 
        registryCredential = 'Dockerhub-id' 
        dockerImage = '' 
    }
    
    stages {
        stage ('Checkout Git'){
         steps{
              git branch :'Farouk',
              url : 'https://github.com/aminetrimech99/Devops.git';
              }
        }
        stage ('MVN Clean')
        {
         steps{
                sh 'mvn clean install'
            }
        }
         stage ('MVN compile')
        {
         steps{
                sh 'mvn compile'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('MVN SonarQube : Tester la qualité') {
            steps {
                withSonarQubeEnv(installationName : 'squareqube_test'){
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('upload to nexus costume repository') {
            steps {
                script{
                def readPomversion = readMavenPom file: 'pom.xml'
                nexusArtifactUploader artifacts: 
                [
                    [
                        artifactId: 'achat',
                        classifier: '',
                        file: 'target/achat-1.0.jar',
                         type: 'jar'
                    ]
                ],
                credentialsId: 'nexus-authid',
                groupId: 'tn.esprit.rh',
                nexusUrl: '192.168.1.18:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'Demoapp-release',
                version: "${readPomversion.version}"
            }
            }
        }
        stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"  
                }
            } 
        }
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up the built image on the local server') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
        
       
    }
}
