pipeline{
   agent any
       stages{
            
         stage ('Github Project'){
               steps{
                  git branch :'MedAliHammami',
                  url : 'https://github.com/aminetrimech99/Devops.git'
              
                   }
            }
         
         stage ('Maven Clean & compile '){
               steps{
                  sh 'mvn clean install'
                   sh 'mvn compile'
                    }
            } 
         
         stage ('Artifact Build'){
               steps{
                   sh 'mvn clean package'
                   }
           }
         stage('Building our image') {
               steps{

            dockerImage = docker.build registry + ":$BUILD_NUMBER"
                  }
}
       }
}
