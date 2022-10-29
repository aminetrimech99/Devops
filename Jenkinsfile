pipeline{
    agent any
    stages{
       stage ('Git'){
         steps{
              git branch :'main',
              url : 'https://github.com/aminetrimech99/Devops.git',
              credentialsId : 'token-for-jenkins-git3'
              
              }
        }
       stage ('build')
        {
         steps{
                sh 'mvn clean install -DskipTests'
            }
        }
    }
}
