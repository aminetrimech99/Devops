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
           stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("getintodevops/hellonode")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
           
       }}
