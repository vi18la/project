pipeline{

    environment{
      dockerimagename = "vidhyasaran/nodeapp"
      dockerImage = ""
    }

    agent any
#checkinout the sourcecode from github
    stages {
       
       stage("checkout source")  {
         steps{
           git 'https://github.com/vi18la/project.git'
         }

       }
#building the image (make sure you install docker pipeline plugin)
       stage("Build image") {
         steps{
           script{
            dockerImage = docker.build dockerimagename
           }
           
         }
       }
#pushing the image to dockerhub(make sure you have configured the creds in jenkins)

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
