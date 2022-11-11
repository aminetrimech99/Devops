pipeline{
                   }
            }

         stage ('Maven Clean'){
         stage ('Maven Clean & compile '){
               steps{
                  sh 'mvn clean install'
                    }
            } 

         stage ('Maven Compile') {
               steps{
                   sh 'mvn compile'
                    }
           }
            } 

         stage ('Artifact Build'){
               steps{
                   sh 'mvn clean package'
                   }
           }
         stage ('Docker'){
               steps{
                   sh 'Docker ps'
                   }
           } 
       }
}
