# Week 1.1 - Build your first application 

In this lab you will create your first Node.js application using Cloud Foundry Public environments. 

  - [Need to know](#need-to-know)
  - [Create your first app](#create-your-first-app)
  - [Summary](#summary)
  

## Need to know

**Runtime**: Set of resources that is used to run an application. Every programming language specifies an execution model, that is why there is Python, PHP, Go, Ruby, Java and many other runtimes. 

**Node.js**: Open-source, cross-platform, JavaScript runtime environment that executes JavaScript code outside of a browser.

**Cloud Foundry**: Open source, multi-cloud application platform as a service (PaaS) governed by the Cloud Foundry Foundation. Cloud Foundry’s container-based architecture runs apps in any programming language over a variety of cloud service providers.

## Create your first app

1. Log-in to IBM Cloud
- https://cloud.ibm.com/login

2. Click the _**Create Resource**_ button at the top right. This action will take you to the 'Catalog'.

<img src="/images/create-resource.png" width="100%" height="100%">

3. Find _**Cloud Foundry**_ under 'Compute' and click on it. 

<img src="/images/cloud-foundry.png" width="50%" height="50%">

4. Select Public applications and click 'Create'. This action will open a new tab. 

_Public Applications_: Deploy apps on IBM Cloud's multi-tenant Cloud Foundry enviroment available in 5 IBM Cloud Regions.
_Enterprise Environment_: Create an isolated, single-tenant, IBM Cloud Foundry Enterprise Environment.

<img src="/images/IBM_create_puclic_applications.png" width="70%" height="70%">

5. Let's configure our application!
- Choose _**London**_ or _**Frankfurt**_ as the region to deploy your application. 
- Select SDK Node.js runtime and the Lite (Free) plan with 256MB of memory.

<img src="/images/configure-cloud-foundry1.png" width="100%" height="100%">
<img src="/images/configure-cloud-foundry-2.png" width="100%" height="100%">

- Give your application a name. The name will be part of your URL to access the application. **Note that this name has to be unique in IBM Cloud**. 

<img src="/images/configure-cloud-foundry-3.png" width="100%" height="100%">

6. Click on 'Create' to start your application. This process will take few minutes. 

<img src="/images/create-application.png" width="40%" height="40%">

7. Once the application is ready you will see a green dot and the message that the application is awake or running. 
Access your application by clicking in the 'Visit App URL'. 

<img src="/images/application-ready.png" width="150%" height="150%">


**Congratulations, you deployed a Hello World application on IBM Cloud™!** :clap:

<img src="/images/nodejs-hello-world.png" width="100%" height="100%">

## Summary

Fantastic! Week 1.1 is complete! :smile:

At this point you have created your first Node.js application on IBM Cloud using Cloud Foundry public environment.
Now that your application is ready go to [Week 1.2 - Enable Delivery Pipeline](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/tree/master/Week%201.2%20-%20Enable%20Delivery%20Pipeline). 
