![image](https://user-images.githubusercontent.com/49730521/87540495-6a22b700-c6bd-11ea-9221-535cfad8261d.png)
## About the task
1. Create Security group which allow the port 80.
2. Launch EC2 instance.
3. In this Ec2 instance use the existing key or provided key and security group which we have created in step 1.
4. Launch one Volume using the EFS service and attach it in your vpc, then mount that volume into /var/www/html
5. Developer have uploded the code into github repo also the repo has some images.
6. Copy the github repo code into /var/www/html
7. Create S3 bucket, and copy/deploy the images from github repo into the s3 bucket and change the permission to public readable.
8 Create a Cloudfront using s3 bucket(which contains images) and use the Cloudfront URL to update in code in /var/www/html

![image](https://user-images.githubusercontent.com/49730521/87540610-a1916380-c6bd-11ea-9758-2aa1a456106d.png)
![image](https://user-images.githubusercontent.com/49730521/87540803-e0bfb480-c6bd-11ea-8adc-eaa3f62f36c5.png)
![image](https://user-images.githubusercontent.com/49730521/87540886-fe8d1980-c6bd-11ea-9489-d425eae9fc3e.png)
![image](https://user-images.githubusercontent.com/49730521/87540949-18c6f780-c6be-11ea-8354-0e6549694950.png)
![image](https://user-images.githubusercontent.com/49730521/87541013-3300d580-c6be-11ea-8a6d-33030de3dcb3.png)
