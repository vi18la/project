# project
project
Deploying application on kubecluster
Setup a docker server
•	Launch an ec2 instance with the default settings.
•	Login to the server via putty.
•	Once logged in become a root user and update the server.
•	Now install Docker on the linux machine, using the below command
1.	Yum install docker –y
2.	Start the service and check the status.
3.	Systemctl start docker
4.	Systemctl status docker.
The status should be active (running)
 
•	Now that we are going to run Jenkins on docker server, by using the Jenkins image from the docker hub.(use the below code)
docker run -u 0 --privileged --name jenkins -it -d -p 8080:8080 -p 50000:50000\
-v /var/run/docker.sock:/var/run/docker.sock \
-v  $(which docker):/usr/bin/docker \
-v /home/jenkins_home:/var/jenkins_home \
jenkins/jenkins:latest
 
•	Check if the image is created , images using docker images command
 
•	Check the status of the docker container using docker ps -a
 
•	Check for the logs using docker logs a207109a5869
•	We can now see that our Jenkins is running on port 8080
•	The initial login password will for jenkins in the path /var/jenkins_home/secrets/initialAdminPassword
•	Login to Jenkins using the creds, and install suggested plugins
•	Once you are into the Jenkins dashboard, create a Jenkins project and configure them as below:
•	Enable “””GitHub hook trigger for GITScm polling””’, 
•	We are enabling it because whenever the developer commits the code to github, the pipeline will start building automatically.
•	Parallely navigate to github to setup webhooks.
•	Go to git repo and click settings
•	Click on webhooks and give add webhooks-->  add webhooks
•	For the payload url give your Jenkins_url/github-webhook/
•	Now navigate back to your pipeline project
•	And in the pipeline section select “”’pipelinescript from scm “’’ and also update your github url,if your repo is public you can ignore creds else provide the creds.
•	Apply and save the project.
•	Go to Jenkins dashboard --> manage Jenkins--> manageplugin-->in the available tab, install-->docker pipeline””” 
•	Now navigate to-->manage Jenkins--> manage  credentials -> global --> add credentials
•	Details of creds:
•	Username : your docker hub username
•	Password: your dockerhub password
•	ID: c/p the name that you mentioned in the Jenkins file and save it. (to push the image to Docker hub, Jenkins will use this creds to get validated).
•	Finally click on your projrct and “”build now””
 

Github link to Docker file, Jenkins file: https://github.com/vi18la/project.git


