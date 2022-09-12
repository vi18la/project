pipeline{

    environment{
      dockerimagename = "vidhyasaran/nodeapp"
      dockerImage = ""
    }

    agent any

    stages {
       
       stage("checkout source")  {
         steps{
           git 'https://github.com/vi18la/project_cliff.git'
         }

       }

       stage("Build image") {
         steps{
           script{
            dockerImage = docker.build dockerimagename
           }
           
         }
       }

       stage("pushing image") {
          environment {
            registryCredential =  "dockerhublogin"
          }
          steps{
            script {
              docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
                 dockerImage.push("latest")
             }
          }
       }
      }
       

}






























 }
