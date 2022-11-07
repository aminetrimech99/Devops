pipeline{
    agent any
    
    stages{
       stage ('Git'){
         steps{
              git branch :'main',
              url : 'https://github.com/aminetrimech99/Devops.git',
              credentialsId: 'git-tokeen'
              
              }
        }
       stage ('MVN Clean')
        {
         steps{
                sh 'mvn clean install -DskipTests'
            }
        }
         stage ('MVN compile')
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
              stage("Publish to Nexus Repository Manager") {
            steps {
                  sh " mvn -f Spring/pom.xml clean package deploy:deploy-file -DgroupId=tn.esprit.rh -DartifactId=achat -Dversion=1.0-SNAPSHOT -DgeneratePom=true -Dpackaging=jar -DrepositoryId=deploymentRepo -Durl=http://192.168.1.26:8081/repository/maven-releases/ -Dfile=target/achat-1.0.jar"
            }
              }
        }
    }

