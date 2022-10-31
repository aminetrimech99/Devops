pipeline{
    agent any
    stages{
       stage ('Git'){
         steps{
              git branch :'main',
              url : 'https://github.com/aminetrimech99/Devops.git',
              credentialsId: 'token-for-jenkins-git'
              
              }
        }
       stage ('build')
        {
         steps{
                sh 'mvn clean install -DskipTests'
            }
        }
         stage ('compile')
        {
         steps{
                sh 'mvn compile'
            }
        }
          stage ('build package')
        {
         steps{
                sh 'mvn package'
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
    }
}
