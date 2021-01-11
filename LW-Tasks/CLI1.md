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

### STEP 3:
## _✨Launching an Instance using above created key pair and Security group_
Now we have to Launch one EC2 Instance using above Key pair and Security Group .To launch ec2 instance AWS CLI has command as :

```
aws ec2 run-instances   --security-group-ids   group_id   --instance-type _type_ --image-id ami_id   --key-name key_name  --count no_of_instance 
```

![8](https://user-images.githubusercontent.com/49730521/96339548-2328d100-10b3-11eb-85b8-ae905246983d.png)

Our instance is now launched in ap-south-1a

![9](https://user-images.githubusercontent.com/49730521/96339555-2d4acf80-10b3-11eb-9bdd-2969eb9df624.png)

### STEP 4:
##  _✨Create an EBS volume of 1 GB_
After Launching EC2 Instance now we have to create one EBS Volume & this volume type will be general purpose SSD Volume.

```
aws ec2 attach-volume --volume-id vol-0ef37a7b52cf3c87b--instance-id i-05bea6de1322b3aec--device /dev/xvdh
```

![10](https://user-images.githubusercontent.com/49730521/96339629-9599b100-10b3-11eb-9c28-451a06785c7d.png)

Our volume is now successfully created and we can see that in the Console of AWS.

![11](https://user-images.githubusercontent.com/49730521/96339644-a5b19080-10b3-11eb-8161-269de86fbb05.png)

### STEP 5:
## _✨ Attach the above created EBS volume to the instance that created in the previous steps._
To Attach EBS Volume to EC2 Instance we have command :
```
aws ec2  attach-volume   --volume-id volume_id   --instance-id instance_id  --device device_name
```
![12](https://user-images.githubusercontent.com/49730521/96339705-017c1980-10b4-11eb-8a9f-a1e10804b486.png)

Our volume is now successfully attached and we can see that in the Console of AWS.

![13](https://user-images.githubusercontent.com/49730521/96339729-0b9e1800-10b4-11eb-8132-71333266a164.png)

### STEP 6:
## _✨At last we have to Terminate the EC2 Instance_
Before Terminating the EC2 Instance, we first Detach the EBS Volume using command

```
aws ec2  detach-volume  --volume-id  volume_id
```
![14](https://user-images.githubusercontent.com/49730521/96339857-c0383980-10b4-11eb-8fc3-8aeed72380ac.png)
To Terminate the EC2 Instance use command :
```
aws ec2 terminate-instances --instance-ids  instance_id
```
![15](https://user-images.githubusercontent.com/49730521/96341022-9bdd5c80-10b6-11eb-8273-2ce6a516f914.png)

## ✨Working with Command Line Environment is always better than Using manual approach of GUI which leads us towards Automation World .
### 🔰 So , In this project,  I have build basic cloud Environment using CLI of AWS Cloud without going to AWS GUI Console .
