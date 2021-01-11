# Week 1 - Introduction, Infrastructure & Compute
## What Is Cloud Computing?
Cloud computing is the on-demand delivery of compute power, database storage, applications, and other IT resources through a cloud services platform via the internet with pay-as-you-go pricing.

## AWS account

  * [Getting Started](https://aws.amazon.com/getting-started/)
  * [Console](https://console.aws.amazon.com/console/home)
  * [Launch a Cloud Server](https://lightsail.aws.amazon.com/ls/webapp)

## AWS Overview

### What is AWS Cloud?

It's an on-demand, pay-as-you go, IT services, delivered over the Internet.


### Six Advantages and Benefits of Cloud Computing

  * Trade capital expenses for variable expense
  * Benefit from massive economies of scale
  * Stop guessing capacity
  * Increase speed and agility
  * Stop spending money on running and maintaining data centers
  * Go global in minutes


### Deployment models

There is a range of deployment models, from all on-premises to fully deploy in the cloud. Many users begin with a new project in the cloud, and they might integrate some on-premises applications with these new projects in a hybrid architecture. They might decide to keep some legacy systems on-premises. Over time, they might migrate more and more of their infrastructure to the cloud, and they might eventually reach an all-in-the-cloud deployment.

[More details](https://aws.amazon.com/types-of-cloud-computing/).


### Products and Services

With over 150 products and services offered by AWS, they cover areas like compute, storage, IoT, security, databases, analytics, networking, mobile, developer tools, management tools and enterprise applications.

The [comprehensive list of products](https://aws.amazon.com/products/).


### AWS Partner Network
APN Partners are focused on your success, and they help customers take full advantage of all the business benefits that AWS has to offer.
Read [more](https://aws.amazon.com/partners/).


### AWS Marketplace 

Is a digital catalog with thousands of software listings from independent software vendors. It offers testing, buying and deploying software on AWS. 

More info on [AWS Marketplace](https://aws.amazon.com/marketplace).


## AWS Infrastructure

How does AWS deploy it's services regionally? The region is a geographically self-contained area which contains all the necessary resources. It's inside a single country boundary, within a single set of laws. 

Every region is designed to be self-contained, with all the assets needed to run my application. To answer which region is appropriate for my app, there are four considerations:

  1. Latency - where are the customers located? 
  2. Cost - not every region is priced the same. Because of different tax laws in different countries. 
  3. Compliance - legal restrictions. Eg. HIPAA or GDPR requirements. 
  4. Service availability - when a brand new feature gets released, it might take a few months to get all the regions around the world.

### What is a region actually made of? 

AWS region is a collection of availability zones. You can think of it like a standalone data center (even though might be multiple data centers). 

Inside a region, there's at least two availability zones, separated by a distance, connected with a high-speed fiber network. It's for redundancy and reliability purposes. 

AWS [global infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)


## Compute

Sample aplication is a corporate directory application, which will serve to demonstrate how different AWS services can work together to build an application. 


### Introduction to Compute Services on AWS

Usually, after estimating the compute capacity needed for our app, we'd buy the hardware to support that capacity and deploy our app on them. After deployment, it's necessary to maintain the servers, both physically and sofware-wise. 

With cloud services, it's possible to use compute-as-service model. That way it's possible to provision and consume raw compute or server capacity with pay-as-you go pricing. Which eliminates the need to maintain the machines. 

The advantage of compute-as-a-service is the fact that it's easier to increase or decrease the capacity, eliminitating the risk in underprovisioning or overprovisioning the resources. 

AWS offers

  * container services, allowing to use Docker through Elastic Container Service (ECS)
  * Kubernetes (EKS)
  * pure serverless solutions - AWS Lambda

Details about the full range of [AWS compute services](https://aws.amazon.com/products/compute/).


### Amazon Elastic Compute Cloud (EC2)

Allows for provisioning of virtual servers on-demand. Each server is called an EC2 instance. 

When setting up an instance, I choose an Amazon Machine Image (AMI), e.g. Linux, Windows. It contains information how the instance needs to be configured, with OS and other software. 

[Features and Cost of EC2](https://aws.amazon.com/ec2/).

### EC2 Instance Types

Amazon EC2 provides a wide selection of instance types that are optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity. They give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes, which allows you to scale your resources to the requirements of your target workload Current details about available instances is [here](https://aws.amazon.com/ec2/instance-types/).


## Amazon Lightsail

is the easiest way to get started with AWS for developers, small businesses, students, and other users who need a simple virtual private server (VPS) solution. Lightsail provides developers compute, storage, and networking capacity, and it also provides capabilities to deploy and manage websites and web applications in the cloud. Lightsail includes everything you need to launch your project quickly--a virtual machine, solid state drive (SSD)-based storage, data transfer, Domain Name System (DNS) management, and a static IP--for a low, predictable monthly price.

  * [Launch video](https://www.youtube.com/watch?v=29_LqYnomdg)
  * [Lightsail](https://aws.amazon.com/lightsail/)
