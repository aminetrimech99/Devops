pipeline{
   agent any
       stages{
            
         stage ('Github Project'){
               steps{
                  git branch :'MedAliHammami',
                  url : 'https://github.com/aminetrimech99/Devops.git'
              
                   }
            }
         
         stage ('Maven Clean'){
               steps{
                  sh 'mvn clean install'
                    }
            } 
         
         stage ('Maven Compile') {
               steps{
                   sh 'mvn compile'
                    }
           }
         
         stage ('Artifact Build'){
               steps{
                   sh 'mvn clean package'
                   }
           }
       }
}
