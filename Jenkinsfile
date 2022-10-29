pipeline{
    agent any
    stages{
       stage ('Git'){
         steps{
              git branch :'main'
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
