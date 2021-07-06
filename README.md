# Tema Final 1 - Trilha Cloud Native

## About this guide:

This is a guide that will help you to:
- Create 3 jobs on Jenkins (1º job - Build app, 2º job - Infra App and 3º job - Run App);
- Execute theses jobs on Jenkins.

## Required:

1. You need to install **Docker**. Please click [here](https://docs.docker.com/engine/install/) to follow the instructions to install Docker.
- After that, you need to create a Dockerhub account. To do that, please click [here](https://hub.docker.com).
- Then, create your public repository.

2. You need to install **Packer**. Please click [here](https://www.packer.io/docs/install) to follow the instructions to install Packer.

1. You need to install **Jfrog**. Please click [here](https://www.jfrog.com/confluence/display/JFROG/Installing+Artifactory) to follow the instructions to install Jfrog.
- After that, open JFrog on your browser and create your user credentials.
- Click on the option Quick Setup (right corner under Welcome) select your new Gradle Repository to create it.

4. You need to install **Jenkins**. Please click [here](https://www.jenkins.io/doc/book/installing/) to follow the instructions to install Jenkins.
- After thar, create a new Jenkins Username and Password and install all recommended plugins.

## Video:

- There is a video that explain the Pipeline process of this repository. Please click [here](https://www.youtube.com/watch?v=rzaKDeLuVlg) to check it out.

## Jenkins Configuration:

1. After you install and create your jenkins Username and password, on Jenkins App go to the tab "Manage Jenkins" and click on "Manage
Plugins", then on Available Tab and use the filter text input to	search for "Artifactory" plugin and select it.
Click on the option "Install without restart".

2. After that, go back to "Manage Jenkins" and click on "Configure System", go to JFrog section and click on "Add Artifactory Server".

1. On the option "Server ID" type: jfrog-artifactory-server

1. On the option "URL" type your artifactory URL.

1. On "Deployer Credentials" enter your JFrog user and password.

1. To check your Jfrog connection, click on "Test Connection".

1. If everything is ok, click on "Save" and go back to "Manage Jenkins" section.

1. On your "Manage Jenkins" section,  click on "Manage Credentials" and then click on "global" domain.

1. Add a Username with Password credential with the following set:
- ID: artifactory-credentials
- Username: (YourArtifactoryUsername)
- Password: (YourArtifactoryPassword)
- Description: JFrog Artifactory Credentials

10. Add a Secret Text Credential with the following set:
- ID: artifactory-url
- Secret: (YourArtifactoryURL)
- Description: JFrog Artifactory Server URL

11. Add a Username With Password credential with the following set:
- ID: dockerhub-credentials
- Username: (YourDockerhubUsername)
- Password: (YourDockerhubPassword)
- Description: Docker Hub Credentials

12. Add a Secret Text Credential with the following set:
- ID: dockerhub-repository
- Secret: (YourPublicDockerhubRepository)
- Description: Docker Hub Repository

## Pipeline:

### Job1 - Build App:

- Create a new job on Jenkins, choose a name for the job and click in the option: Pipeline.
- On the tab "Advanced Project Options", go to "Definition" and select the option "Pipeline Script from SCM".
- After that, on "SCM" select the option "Git". Then paste this link: https://github.com/MatheusSantana95/finalTheme1. 
- On the option "Branch Specifier (blank for 'any')", type ```*/main```.
- Finally, click on save.

### Job2 - Infra App:

- Create a new job on Jenkins, choose a name for the job and click in the option: Pipeline.
- On the tab "Advanced Project Options", go to "Definition" and select the option "Pipeline Script from SCM".
- After that, on "SCM" select the option "Git". Then paste this link: https://github.com/MatheusSantana95/tema-final1-Ansible-Packer. 
- On the option "Branch Specifier (blank for 'any')", type ```*/main```.
- Finally, click on save.

### Job3 - Run App:

- Create a new job on Jenkins, choose a name for the job and click in the option: Pipeline.
- On the tab "Advanced Project Options", go to "Definition" and select the option "Pipeline Script and paste the Jenkinsfile script located at "job3-RunApp" folder of this project.
Finally, click on save.

## Building the jobs:

1. Go to your jenkins "Dashboard" and select the first job that you´ve created and select the option "Build now".
- Wait until the proccess finish. 
- If you receive the message "SUCCESS", your job was build successfully. 
- If you received the message "FAILURE", please repeat all the proccess of this tutorial carefully.

2. Go to your jenkins "Dashboard" and select the second job that you´ve created and select the option "Build now".
- Wait until the proccess finish. 
- If you receive the message "SUCCESS", your job was build successfully. 
- If you received the message "FAILURE", please repeat all the proccess of this tutorial carefully.

3. Go to your jenkins "Dashboard" and select the third job that you´ve created and select the option "Build now".
- Wait until the proccess finish. 
- If you receive the message "SUCCESS", your job was build successfully. 
- If you received the message "FAILURE", please repeat all the proccess of this tutorial carefully.

## How to use the Application:

- This application just accepts Http request GET. So to use the Calculator and do some operation, you need to make a GET request.
- To do that, you need to inform the parameters in the URL, for example: http://localhost:8083/rxnetty/rxnetty/?num1=[InsertFirstNumberHere]&num2=[InsertSecondNumberHere]&op=[InsertOperationHere].
- To see the Calculator historic, please type: http://localhost:8083/rxnetty/rxnetty/history.
- To use this application to do math operations, this application just accepts three parameters: num1, num2 and op.
- To use this application to consult the historic for your math operations that you`ve made, this application just accepts the paramether: history.
- This application just accepts the following operations: sum, subtract, multiply, division, and pow.