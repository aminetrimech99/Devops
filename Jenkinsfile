pipeline{
   agent any
       stages{
            
         stage ('Git'){
               steps{
                  git branch :'MedAliHammami',
                  url : 'https://github.com/aminetrimech99/Devops.git',
              
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
         
         stage ('Build Packages'){
               steps{
                   sh 'mvn clean package'
                   }
           }
       }
}
