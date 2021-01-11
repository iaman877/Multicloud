# Week 5 - Security, Cost Management and Course Conclusion
## Amazon Shared Responsibility Model

Security and compliance are shared responsibilities between us and the customer. This shared model can help relieve a customer’s operational burden because we operate, manage, and control the components from the host operating system and virtualization layer down to the physical security of the facilities where the service operates. The customer is responsible for--and manages--the guest operating system (including updates and security patches) and other associated application software, in addition to the configuration of the AWS-provided security group firewall. Customers should carefully consider the services that they choose because their responsibilities will vary depending on the services that they use, the integration of those services into their IT environment, and applicable laws and regulations. The nature of this shared responsibility also provides the flexibility and customer control that permits the deployment. This differentiation of responsibility is commonly referred to as Security of the Cloud versus Security in the Cloud.

## AWS responsibility

AWS is responsible for security of the host operating system, virtualization layer down to the physical security of the facilities where the services operate. The customer is responsible and manages the guest OS, applications running. This is called the "shared security". The difference is often referred to as "Security *of* the Cloud" vs "Security *in* the Cloud".

[More info about the shared security model](https://aws.amazon.com/compliance/shared-responsibility-model/)

## Cost Management in AWS
Security of the Cloud: We are responsible for protecting the infrastructure that runs all of the services that are offered in the AWS Cloud. This infrastructure is composed of the hardware, software, networking, and facilities that run AWS Cloud services.

## Customer responsibility
Security in the Cloud: Customer responsibility will be determined by the AWS Cloud services that a customer selects. This determines the amount of configuration work the customer must perform as part of their security responsibilities.

## AWS Pricing Calculator
AWS has announced a new pricing tool, the AWS Pricing Calculator. This new tool, which is currently in beta, can be used to calculate Amazon EC2 and Amazon EBS pricing. For further information about this tool, see this blog post. For other services, you can use the AWS Simple Monthly Calculator.

## AWS Cost Explorer
AWS Cost Explorer lets you visualize, understand, and manage your AWS costs and usage over time. You can create custom reports (including charts and tabular data) that analyze cost and usage data, both at a high level (e.g., total costs and usage across all accounts) and for highly specific requests (e.g., m2.2xlarge costs within account Y that are tagged project: secret Project).

## AWS Trusted Advisor
AWS Trusted Advisor is an online resource to help you reduce costs, increase performance, and improve security by optimizing your AWS environment. Trusted Advisor provides real-time guidance to help you provision your resources by following our best practices.

There are multiple cost management tools available in the AWS Management console.

  * [AWS Price Calculator](https://calculator.aws/#/); can be used to get pricing for EC2 and EBS usage, currently in beta; [blog post](https://aws.amazon.com/blogs/aws/check-it-out-new-aws-pricing-calculator-for-ec2-and-ebs/), for other uses, the [AWS Simple Monthly Calculator](https://calculator.s3.amazonaws.com/index.html) can be used 
  * [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/); allows visualizing and understanting cost and usage, it can also generate reports
  * AWS Budgets, allows creating alerts when the cost exceed the threshold set
  * [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/trustedadvisor/); can help reduce cost, increase performance and security, increase fault tolerance


  
    
