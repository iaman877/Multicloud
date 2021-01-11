# What is Auto Scalling 
Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.
## Critical Question 
1. How can I ensure that my workload has enough EC2 resources to meet fluctuating performance requirements?
2. How can I automate EC2 resource provisioning to occur on-demand?
### Auto Scalling Components
1. Launch Configuration	: what 
    1. AMI
    2. Instance type 
    3. Security Grpup
    4. Role
2. Auto Scaling Group   : where
   1. VPC and Subnet(s)
   2. Load balancer 
   3. Minimum instance 
   4. Maximum instance
   5. Desired capacity
3. Auto Scaling Policy    : when 
   1. Scheduled 
   2. On-demand 
   3. Scale-out-policy
   4- Scale-down-policy
