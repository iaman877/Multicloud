# Day 3 Topic Covered

1. 👉What is the Availability Zone?
1. 👉What are the regional services?
1. 👉What is RDP?
1. 👉Role of Aws security group in creating a user trusted cloud?
1. 👉How port no is a way to host the client on the AWS cloud ?
1. 👉How a user can connect to windows OS via RDP?
1. 👉Why key is used in Linux is and password for windows?
1. 👉What are the main things you require to connect through RDP?
1. 👉 Do putty support .pem format private key?
1. 👉What are security groups?
1. 👉Role of security group?
1. 👉How to create inbound rules ?

## Soultion 
1. An Availability Zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity in an AWS Region.
1. AWS provides a lot of services and these services are either Global, Regional or specific to the Availability Zone and cannot be accessed outside. Most of the AWS managed services are regional based services (except for IAM, Route53, CloudFront, WAF etc).
1. Amazon EC2 instances created from most Windows Amazon Machine Images (AMIs) enable you to connect using Remote Desktop. Remote Desktop uses the Remote Desktop Protocol (RDP) and enables you to connect to and use your instance in the same way you use a computer sitting in front of you. It is available on most editions of Windows and available for Mac OS.
1. A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic. Inbound rules control the incoming traffic to your instance, and outbound rules control the outgoing traffic from your instance. When you launch an instance, you can specify one or more security groups.
1. https://docs.aws.amazon.com/workspaces/latest/adminguide/workspaces-port-requirements.html
1. In the Amazon EC2 console, select the instance, and then choose Connect. In the Connect To Your Instance dialog box, choose Get Password (it will take a few minutes after the instance is launched before the password is available).
1. In linux putty supports key , while using RDP client supports password which we get after decryption.
1. to connect throught RDP protocal we need a software which supports RDP protocol which is RDP client which asks for userid ipaddress and password.
1. PuTTY doesn't natively support the private key format (. pem) generated by Amazon EC2. You must convert your private key into a . ppk file before you can connect to your instance using PuTTY.
1. Apart from the authentication, there is one more security measure which is known as Firewall. In AWS it is known as Security Group.
1. An IAM role is an IAM entity that defines a set of permissions for making AWS service requests. IAM roles are not associated with a specific user or group. Instead, trusted entities assume roles, such as IAM users, applications, or AWS services such as EC2 "There are two kinds of rules: Inbound/Ingress and Outbound/Egress "
1. Inbound means incoming traffic coming to your EC2 instances.
For that you have to add inbound rule. For web server generally we use port 80. Outbound means outgoing traffic from your EC2 instances. To connect internet or any browser you have to add outbound rule
