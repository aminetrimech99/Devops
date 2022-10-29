pipeline{
    agent any
    stages{
       stage ('Git'){
         steps{
              git branch :'main',
              url : 'https://github.com/aminetrimech99/Devops.git',
              credentialsId : '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'
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
