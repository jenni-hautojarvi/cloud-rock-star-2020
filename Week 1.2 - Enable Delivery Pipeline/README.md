# Week 1.2 - Enable Delivery Pipeline

In this lab you will create your first Node.js application using Cloud Foundry Public environments. 

  - [Need to know](#need-to-know)
  - [Enable delivery pipeline](#enable-delivery-pipeline)
  - [Configure delivery pipeline](#configure-delivery-pipeline)
  - [Summary](#summary)
  

## Need to know

**DevOps**: Set of practices that combines software development (Dev) and information-technology operations (Ops) which aims to shorten the systems development life cycle and provide continuous delivery with high software quality.

**Delivery Pipeline**: Automates the continuous deployment of a project. In a project's pipeline, sequences of stages retrieve input and run jobs, such as builds, tests, and deployments.

**Toolchain**: A set of tool integrations that support development, deployment, and operations tasks. The collective power of a toolchain is greater than the sum of its individual tool integrations.

**Git**: Distributed version-control system. With Git, you can track changes to your content and collaborate on it with your team in an agile way. Git is fast because its repos are stored locally instead of on a remote computer. Some people consider Git to be the lingua franca of version control.

**Repository**: A software repository, or “repo” for short, is a storage location for software packages. Often a table of contents is stored, source code, as well as metadata. 

## Enable delivery pipeline

1. Go to your application's 'Overview' page. 

<img src="/images/application-overview.png" width="100%" height="100%">

If you closed your application tab you can go to IBM Cloud dashboard -> Cloud Foundry Apps -> Your application.

Here you can see your Node.js application status, memory, instances, connections with other services even costs. 

<img src="/images/application-stats.png" width="100%" height="100%">

2. Go down and you will find the 'Continuous Delivery' box. Click on 'Enable'. 

<img src="/images/continuos-delivery.png" width="50%" height="50%">

This action will open a new tab.

## Configure continuous delivery toolchain

3. Let's configure the toolchain

- By default the toolchain's name will be the same as your application
- Make sure the toolchain region is the same as the one you selected for your application. 
- Set resource group as 'Default'. Each toolchain is associated with a specific region and resource group.

<img src="/images/congfigure-toolchain.png" width="100%" height="100%">

Under tool integrations your will see 3 options:
 - Git Repos and Issue tracking
 - Delivery Pipeline
 - More tools
 
4. Git repos and issue tracking
Git allow you to store and manage your code and track your work, including defects, enhancements, and tasks.
Collaborate with your team and manage your source code with a Git repository (repo) and issue tracker that is hosted by IBM and built on GitLab Community Edition.

In this section we will clone the repositoty to the IBM Cloud to have all our code available in the cloud. 
Access to Git Repos and Issue Tracking repositories is region-specific so make sure you have the right region. 

<img src="/images/congfigure-git-issues.png" width="100%" height="100%">

5. Delivery Pipeline
Helps you automatically build and deploy to IBM Cloud.

- Create an API key by clicking in the 'New' button. The pipeline uses an IBM Cloud API key that you provide to access cloud services on your behalf.

<img src="/images/configure-delivery-pipeline.png" width="90%" height="90%">

- A pop-up window will give you more information about the API key and how to manage access to the delivery pipeline. Click 'OK'.

<img src="/images/configure-delivery-pipeline2.png" width="50%" height="50%">

6. More tools
There is no configuration in the more tools tab. 
This tab will automatically add Eclipse IDE to our toolchain.
The Eclipse Orion Web IDE is a web-based, integrated development environment where you can create, edit, run, debug, and perform source-control tasks. You can seamlessly move from editing to running to submitting to deploying.

<img src="/images/configure-more-tools.png" width="90%" height="90%">

7. Once the toolchain is configured click on the top right corner 'Create' button. 

<img src="/images/create-toolchain.png" width="100%" height="100%">

Several steps run automatically to set up your toolchain:
- The toolchain is created.
- The sample repo is cloned into your Git Repos and Issue Tracking account. You now have your own version of the code.
- The delivery pipeline is created and triggered.
- The toolchain is associated with your app. When you push changes to the toolchain's repo, the delivery pipeline automatically builds and deploys the app.

After a few moments, your new toolchain's Overview page opens.

<img src="/images/toolchain-ready.png" width="80%" height="80%">

**Congratulations, you created your first toolchain on IBM Cloud™!** :clap:

## Summary

Week 1.2 is complete! Congrats! :smiley:

In this lab you starter your DevOps journey enabling a delivery pipeline for your application. 

<img src="/images/toolchain.png" width="70%" height="70%">

Now that your delivery pipeline is ready go to [Week 1.3 - Modify your application](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/tree/master/Week%201.3%20-%20Modify%20your%20application). 
