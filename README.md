Section 1 - Code was stored on my local machine then stored on GitHub which was then pull via the use of Jenkins and with the help of maven this source code was then build which also produced us with artifacts 
![screenshot-www udemy com-2024 04 17-11_33_45](https://github.com/Sehindemi/hello-world/assets/97199481/c5c99673-acd4-41cc-bfff-2baf821eaa6c)


Section 2 -
Code was stored on local machine then stored on GitHub which was then pull via the use of Jenkins and with the help of maven this source code was then build which also produced us with artifacts, and this artifacts is then deployed onto the tomcat EC2 target server environment.

I Implemented a Automated build and deploy within the Job configuration by  using the poll SCM to ensure whenever i made a commit on my source repository the changes will then be pull by jenkins and would be built by jenkins.
![screenshot-www udemy com-2024 04 17-11_32_52](https://github.com/Sehindemi/hello-world/assets/97199481/33338bd1-62db-4162-b1a8-4d3effea35f1)

Section 3 
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

