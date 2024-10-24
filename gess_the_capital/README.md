# Deploy-an-Application-on-Cloud
Building a docker container image, upload it to IBM Cloud Container Registry, and deploy an application on cloud  using a serverless technology called IBM Code Engine! 

# Objectives:
Clone the source code
Build Docker image
Deploy on Docker
Tag and Push image to IBM Cloud
Deploy on IBM Code Engine

#Docker
Containers are isolated environments that package applications and their dependencies. Each container runs as an isolated process on the host operating system.

Docker is an open-source platform that enables developers to automate the deployment and management of applications inside lightweight, isolated containers.

# IBM Cloud
IBM Cloud is a cloud computing platform and suite of cloud-based services offered by IBM. It provides a range of infrastructure, platform, and software services to support the development, deployment, and management of various types of applications and workloads in the cloud.

# IBM Code Engine
IBM Cloud Code Engine is a serverless compute platform provided by IBM Cloud. It allows developers to deploy and run containerized applications without the need to manage the underlying infrastructure. Abstracting away the complexities of server provisioning, scaling, and maintenance, enabling developers to focus on writing code and building applications.

#Step 1
Verify that docker CLI is installed.
Of terminal and type

> Command to Check:
>
>       docker --version

#Step 2
Verify that ibmcloud CLI is installed.

Again in terminal
> Command to Check:
>
>     ibmcloud version

# Start Code Engine
#Step 3
On the menu select Code Engine. The code engine setup panel appears. Click Create Project to begin.
![image](https://github.com/user-attachments/assets/a9c3bc59-2533-4312-a673-196464114dfe)


#Step 4
The code engine environment takes a while to prepare. You will see the progress status is indicated in the setup panel.
![image](https://github.com/user-attachments/assets/685fdbac-72a6-49b7-adda-74d7640bff37)


#Step 5
Once the code engine set up is complete, you can see that it is active. Click Code Engine CLI to begin the pre-configured CLI in the terminal as shown below.
![image](https://github.com/user-attachments/assets/59ce999f-b36a-4b09-bb24-813b462e6fd4)

#Step 6
You will observe that the pre-configured CLI startup and the home directory are set to the current directory. As a part of the pre-configuration, the project has been set up, and Kubeconfig is set up. The details are shown on the terminal as follows.
![image](https://github.com/user-attachments/assets/292a9c13-0f88-46af-b43c-6b45da6aca34)

#Step 6
# Set-up : Create application
Open a terminal window by using the menu in the editor: Terminal > New Terminal.
![image](https://github.com/user-attachments/assets/faab3dc9-74ed-48f2-be60-410ef49d6211)

At this point
Enter Git Commands to clone your existing repo. or import your already developed application.
<b>After sucessfully Importing your application follow below steps</b>

<h2> Task 1: Containerise the application <h1>
Let’/s start modernising our application. The first step towards it is to containerise it using Docker.

<h3>Create Dockerfile</h3>

tasks:

Paste the following content in
"Open Dockerfile in IDE"

> Use the below as Dockerfile content.
>
>     FROM nginx
>     COPY favicon.ico /usr/share/nginx/html/favicon.ico
      COPY index.html /usr/share/nginx/html/index.html
      COPY script.js /usr/share/nginx/html/script.js
      COPY style.css /usr/share/nginx/html/style.css
      COPY data.json /usr/share/nginx/html/data.json

And it should look like below:

![image](https://github.com/user-attachments/assets/e7a9bbed-1016-47e8-9f2a-749a4006ea28)


<h3>Build an image from a Dockerfile</h3>

> Following Code
>
>     docker build -t Your Project Name .



![image](https://github.com/user-attachments/assets/c4ae1869-7831-4bdd-ab82-afb4a5b89083)


<h3>list Built Images</h3>

> Following Code
>
>     docker images .

![image](https://github.com/user-attachments/assets/10ea58cd-c6e6-4e1b-b1c3-7c2b1eaaeae5)


<h3>Run the image</h3>

> Following Code
>
>     docker run -it -d -p 8080:80 Your App Name
> 
![image](https://github.com/user-attachments/assets/6809066e-42c3-4b54-b56b-2c7563f36b4a)


<h4>Must Check for the port for server should be 8080 or what you've put, test lauch your app.</h4>

<h2>Task 2: Deploy on IBM Cloud</h2>
Let’s start with launching Code Engine CLI.

![image](https://github.com/user-attachments/assets/d448065b-b6a1-4ed0-aef6-667e89010489)


<h4>Push the image to IBM Cloud</h4>

> Type
>
>     docker push us.icr.io/${SN_ICR_NAMESPACE}/Your-App-Name

![image](https://github.com/user-attachments/assets/9e4648f3-3b9a-423b-b7e6-a080463306b7)


<h4>Deploy the image on IBM CE</h4>

> Type
>
>     ibmcloud ce application create --Your-App --image us.icr.io/${SN_ICR_NAMESPACE}/Your-App --registry-secret icr-secret --port 80

![image](https://github.com/user-attachments/assets/4a35e0d5-269d-40de-bbcd-46400244fcc3)

<h4>Take Cloud URL from the output; which looks something like: https://Your_app.somerandomalphanumeric.us-south.codeengine.appdomain.cloud and open in your browser.</h4>

# Congratulations
You have completed the deployment and learned how to deploy and host a standard application in Docker and on IBM Cloud.

# Author

Shudhanshu Ranjan

