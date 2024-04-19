Section - 1 - 
![screenshot-www udemy com-2024 04 17-11_33_45](https://github.com/Sehindemi/hello-world/assets/97199481/c5c99673-acd4-41cc-bfff-2baf821eaa6c)
Code was stored on my local machine then stored on GitHub which was then pull via the use of Jenkins and with the help of maven this source code was then build which also produced us with artifacts 



Phase - 2 
![screenshot-www udemy com-2024 04 17-11_32_52](https://github.com/Sehindemi/hello-world/assets/97199481/33338bd1-62db-4162-b1a8-4d3effea35f1)
Code was stored on local machine then stored on GitHub which was then pull via the use of Jenkins and with the help of maven this source code was then build which also produced us with artifacts, and this artifacts is then deployed onto the tomcat EC2 target server environment.

I Implemented a Automated build and deploy within the Job configuration by  using the poll SCM to ensure whenever i made a commit on my source repository the changes will then be pull by jenkins and would be built by jenkins.


Phase - 3 
![screenshot-www udemy com-2024 04 19-18_21_37](https://github.com/Sehindemi/hello-world/assets/97199481/6f6d92e7-2b90-4706-8547-a9f6214ac752)
This time instead of storing deploying the code onto the tomcat server i made sure the code is now deployed onto the a docker container.

Issues faced 
Ran across an issue with tomcat w0 where i got an error http 404 when trying to access the apache container, resolved this issue by logging onto the apache container and moving the content from webapps.dist onto the default webapps which is used for our default apache page 

Resolving the issue permanently 
So to resolve this issue i created a docker file using the tomcat image and copied the /usr/local/tomcat/webapps.dist/* to  /usr/local/tomcat/webapps to prevent this issue from occurring again 

- Used Publish over ssh plugin on Jenkins to ensure we can publish and send artifacts over ssh 
Issues faced
- I had to integrate my docker host with Jenkins and with the plugin this was possible and i was able to integrate the two successful via password authentication 
- After the integration of docker host and jenkins i made sure the .war file gets sent to the /opt/docker folder which also consists of of docker file so when changes are made to the docker file the build will start automatically due to the poll SCM I set up previously.
- Also i set up a post build command which would change directory to the /opt/docker directory and will build the docker image from the docker file thats been pushed and then run a container based of that image


Phase - 4
![image](https://github.com/Sehindemi/hello-world/assets/97199481/b0f8f317-fb65-4d20-a6b0-e8e87ea641f7)
Summary 
I decided to improve this pipeline by making use of ansible which is a deployment tool the goal of using this is to make the pipeline a bit smoother and cleaner 

Jenkins will take the code from github and build artifacts and these artifacts would be coppied onto the ansible server, from this ansible will then create the image with the help of Docker file from the artifacts and then this docker image can be committed onto dockerhub.
So now we can execute a ansible playbook then the ansible host will communicate wit docker hub to pull the image and then run it on a container from it.

Process taken to manage Docker-Host with Ansible
Docker host to ansible, so our ansible control node would be able to manage the docker host. This would be done by creating ssh keys on the ansible host and sending this key onto the docker server which would then allow us to send artifacts to the docker host during the build job phase 

Wrote a playbook to achieve this, within this playbook it'll tell the docker host how to create a docker container, this would be done by adding the docker host onto the ansible inventory file we'll be able to achieve this 

Process of Integrating Ansible with Jenkins 
I integrate Jenkins with Ansible, so Jenkins will be able to copy the artifacts onto the Ansible systems and then It'll be able to create Images or deploy the containers on the docker host.

What this solves:
With this We'll know Jenkins and Maven would solely be responsible for the build activities and ansible would be responsible for the deploy activities 

Used Ansible to create images containers
Made ansible playbooks which would be used to build the docker images with the help of the docker file

Will make ansible push the images onto docker hub which then our docker host server would pull the images from our docker hub and then create a container out of it whenever there's a new code commit on our GitHub repository 

Jenkins Job Overview
![image](https://github.com/Sehindemi/hello-world-CICD-Project/assets/97199481/eb01bb83-4a0d-4c5e-8d62-419942bbfef2)

RegApp Deployment 
![image](https://github.com/Sehindemi/hello-world-CICD-Project/assets/97199481/f6900beb-b824-463f-b523-8559497bd93f)


