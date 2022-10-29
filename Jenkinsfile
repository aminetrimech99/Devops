pipeline{
    agent any
    stages{
       stage ('Git'){
         steps{
            echo 'Pulling ..';
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
