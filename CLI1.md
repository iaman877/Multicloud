# Building AWS Cloud Infrastructure Using AWS CLI
## What is AWS CLI ?
The AWS Command Line Interface (CLI) is a tool to manage AWS services. AWS CLI provides us with a tool to configure control and automate AWS services through scripts and commands.
### Project Description - AWS CLI👨🏻‍💻
* Create a key pair  
* Create a security group  
* Launch an instance using the above created key pair and security group.
* Create an EBS volume of 1 GB. 
* The final step is to attach the above created EBS volume to the instance you created in the previous steps.

⚡ To use AWS CLI, we need to download and install it on the top of Operating System,
```
aws --version
```

⚡ To perform the above task assigned, we need to configure the IAM - User profile that I have already created earlier. & we can also configure our own aws profile by providing access key Id , Secret key Id , region.

![3](https://user-images.githubusercontent.com/49730521/96339322-a77a5480-10b1-11eb-89db-d0bc0a8443ae.png)

### STEP 1:
##            _✨ Creating a Key pair_
 Now we successfully Logged In to AWS Account . After these We have to create Private Key to connect to the ec2 Instance . For creating Key Pair we have command as :
 
 ```
 aws ec2 create-key-pair --key-name iaman
 ```
 
 ![4](https://user-images.githubusercontent.com/49730521/96339422-36876c80-10b2-11eb-9a60-542736cb0a56.png)
 
 Now, we have our keypair ready and we can see that on the console too. 'iaman' is created successfully.
 
 
![5](https://user-images.githubusercontent.com/49730521/96339452-65054780-10b2-11eb-9dcc-8a194a606a48.png)

### STEP 2:
##  _✨Creating a Security group_
A security group acts as a virtual firewall for your instance to control inbound and outbound traffic, to create Security group we have the command as  :
```
aws ec2 create-security-group --group-name  <value>  --description  <value>
```
![6](https://user-images.githubusercontent.com/49730521/96339494-b7466880-10b2-11eb-8c50-f577404c11c6.png)

So, we have our security group created.

![7](https://user-images.githubusercontent.com/49730521/96339502-c5948480-10b2-11eb-813a-f5b651f7a691.png)
