pipeline{
    agent any
    stages{
       stage ('Git'){
         steps{
             sh "git clone https://github.com/aminetrimech99/Devops.git"
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
