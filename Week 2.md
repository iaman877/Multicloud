# Week 2 - Networking and Storage on AWS

## CIDR Notation
An important concept that's used in networking on AWS is CIDR, or Classless Inter-Domain Routing. CIDR network addresses are allocated in a virtual private cloud (VPC) and in a subnet by using CIDR notation. A /16 block provides 65,536 IPv4 addresses. A /24 block provides 256 addresses.
[Article](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)
## Amazon Virtual Private Cloud (VPC)

Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including the selection of your own IP address range, the creation of subnets, and the configuration of route tables and network gateways. You can use both IPv4 and IPv6 in your VPC for secure and easy access to resources and applications. You could create up to five non-default VPCs per AWS account per Region. (See below for information about default VPCs.)

To build a VPC I need to specify two things:

  1. The region
  2. IP range for the private range of IPs which are going to run inside this VPC

For example, IP range can be 10.10.0.0/16. First subnet could then be 10.10.1.0/24 (24 means first 24 bits are frozen in CIDR notation).

To allow website being accessed, we need to add a gateway - IGW (Internet Gateway). It also needs a route table, associated with the subnet. 0.0.0.0/0 represents the traffic from the internet. Even though this can be done manually, in production environment is suggested that be done programatically. Once all of this is set up, EC2 instance can be set up.

After the EC2 instance is set up on the VPC, we'd want to add the database to it. It shouldn't go to the same public subnet, since we don't want direct access to the DB. That requires another subnet (private), which doesn't have access to the IGW - 10.10.2.0/24.

High availability means moving away from a single AZ. Which means creating 2 new subnets in a different AZ. Once they're created, it's necessary to associate them with the routing table we have. After that we create another EC2 instance and a RDS in the second AZ. Since we have 2 EC instances in 2 subnets, we need an Elastic Load Balancer (ELB). 

To communicate with internal objects, not available over the internet, we'd use Virtual Private Gateway (VGW), which can be associate with private subnets. 



### Subnets
A VPC spans all the Availability Zones in the Region. After creating a VPC, you can add one or more subnets in each Availability Zone. When you create a subnet, you specify the CIDR block for the subnet, which is a subset of the VPC CIDR block. Each subnet must reside entirely within one Availability Zone, and it can't span Availability Zones.
Security in a VPC is provided by using Security Groups and Network Access Control Groups. We will talk about AWS Security in a later module.

[Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)

### Default VPC

AWS will provide a default VPC with a /16 CIDR block (65,536) addresses plus /20 subnet for each AZ in the region which provides 4,096 addresses per subnet, with a few reserved for AWS use. You can modify or delete the default VPC. [More info](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html)


## Storage

  * S3 is OBJECT level storage
  * RDS is BLOCK level storage

### Amazon Elastic Block Store (Amazon EBS)

Most common block storage. It provides persistent block storage volumes for use with EC2 instances. Each EBS volume is automatically replicated inside of AZ. Main two categories are SDD (DBs and boot volumes, performance depends on IOPS) and HDD volumes (MapReduce, log processing, performance depends on MB/s).

  * [Documentation](https://aws.amazon.com/ebs)
  * [Pricing](https://aws.amazon.com/ebs/pricing/)

## Amazon Simple Storage Service (Amazon S3)

Amazon Simple Storage Service (Amazon S3) stores data as objects within resources that are called buckets. You can store as many objects as you want within a bucket, and you can write, read, and delete objects in your bucket. Objects can be up to 5 TB in size.
You can control access to both the bucket and the objects (who can create, delete, and retrieve objects in the bucket for example), and view access logs for the bucket and its objects. You can also choose the AWS Region where a bucket is stored to optimize for latency, minimize costs, or address regulatory requirements.
With Amazon S3, you pay only for what you use. There is no minimum fee. Estimate your monthly bill by using the AWS Simple Monthly Calculator. We charge less where our costs are less, and prices are based on the location of your Amazon S3 bucket.


  * [Documentation](https://aws.amazon.com/s3)
  * [Price Calculator](https://calculator.s3.amazonaws.com/index.html)

## Amazon Elastic File System (Amazon EFS)
Amazon Elastic File System (Amazon EFS) provides simple, scalable, elastic file storage for use with AWS Cloud services and on-premises resources. It is straightforward to use, and it offers a simple interface that allows you to create and configure file systems quickly and easily.
Amazon EFS is designed to provide massively parallel shared access to thousands of Amazon EC2 instances. This enables your applications to achieve high levels of aggregate throughput and IOPS that scale as a file system grows, with consistent low latencies.
When an Amazon EFS file system is mounted on Amazon EC2 instances, it provides a standard file system interface and file system access semantics, which allows you to seamlessly integrate Amazon EFS with your existing applications and tools. Multiple Amazon EC2 instances can access an Amazon EFS file system at the same time, thus allowing Amazon EFS to provide a common data source for workloads and applications that run on more than one Amazon EC2 instance


[Documentation](https://aws.amazon.com/efs/)
