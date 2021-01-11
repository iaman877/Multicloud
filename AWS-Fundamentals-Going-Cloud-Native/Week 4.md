# Week 4 - Monitoring and Scaling

Modern applications are often modular, folowing service-oriented or microservices architecture. It's important to have insight into current state of infrastructure and applications. 

## Monitoring and Amazon CloudWatch
Amazon Cloud Watch is a monitoring service for AWS Cloud resources and the applications that you run on AWS. You can use Amazon Cloud Watch to collect and track metrics, collect and monitor log files,
set alarms, and automatically react to changes in your AWS resources.

  * [CloudWatch](https://aws.amazon.com/cloudwatch/)
  * [CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html)
  * [CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)

## Amazon Cloud Watch Events
Amazon Cloud Watch Events delivers a near real-time stream of system events that describe changes in AWS resources. Using simple rules that you can quickly set up, you can match events and route them to one or more target functions or streams.
Cloud Watch Events becomes aware of operational changes as they occur.

## Amazon Cloud Watch Logs Metrics
You can use Amazon Cloud Watch Logs to monitor, store, and access your log files from Amazon EC2 instances, AWS Cloud Trail, Amazon Route 53, and other sources. 
You can then retrieve the associated log data from Cloud Watch Logs.

You can collect metrics from servers by installing the Cloud Watch agent on the server. You can install the agent on both Amazon EC2 instances and on-premises servers,
and on servers that run either Linux or Windows Server.
## Load Balancing

Elastic Load Balancing, ELB, is a regional service, launched inside the VPC. It can perform network load balancing or application load balancing, on the parts of the application. It can also be used internally, like between a fleet of web servers and the application tier. 

It can handle traffic within one or more AZs. It offers three types of load balancers:

  1. Application Load Balancer; operates on request level (Layer 7), routing traffic to targets, like EC2 instances, microservices and containers within VPC, based on the content of the request. Ideal for advanced load balancing of HTTP(s) traffic.

  2. Network Load Balancer; operates at connection level (Layer 4), routing connection to targets like EC2 instances, microservices and containers within VPC, based on IP protocol data. Ideal for load balancing TCP traffic.

  3. Classic Load Balancer operates both on connection and request level, and provides load balancing between multiple EC2 instances.

[Documentation](https://aws.amazon.com/elasticloadbalancing/) 


## Auto Scaling 

Amazon EC2 Auto Scaling helps you maintain application availability, and it allows you to dynamically scale your Amazon EC2 capacity up or down automatically according to conditions that you define. You can use Amazon EC2 Auto Scaling for fleet management of Amazon EC2 instances, which can help maintain the health and availability of your fleet, and ensure that you are running your desired number of Amazon EC2 instances. You can also use Amazon EC2 Auto Scaling to dynamically scale Amazon EC2 instances. Dynamic scaling automatically increases the number of Amazon EC2 instances during demand spikes to maintain performance and decrease capacity during lulls, which can help reduce costs. Amazon EC2 Auto Scaling is well-suited to applications that have stable demand patterns, or applications that experience hourly, daily, or weekly variability in usage.
