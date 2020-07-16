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
_____________________________________________________________________________________________________________________
### Terraform file:
```
provider "aws" {
  region     = "ap-south-1"
  profile = "aman"
}
resource "tls_private_key" "private_key" { 
  algorithm   = "RSA"
  rsa_bits = "2048"
}
resource "aws_key_pair" "task-2-key" {
  depends_on = [ tls_private_key.private_key, ]
  key_name   = "dev-key"
  public_key = tls_private_key.private_key.public_key_openssh
}
```
![image](https://user-images.githubusercontent.com/49730521/87636503-7b6fd000-c75e-11ea-8db7-7b67db301cc3.png)
create a Security group with http,ssh,NFS enable 
```
resource "aws_security_group" "allow_http_NFS" {
  name        = "allow_http"
  description = "Allows http and ssh NFS"
  vpc_id      = "vpc-fa7e6292"


  ingress {
    description = "HTTP allow"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    description = "NFS"
    from_port   = 2049
    to_port     = 2049
    protocol    = "tcp"
    cidr_blocks = [ "0.0.0.0/0" ]
}
  ingress {
    description = "ssh"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
```
![image](https://user-images.githubusercontent.com/49730521/87540803-e0bfb480-c6bd-11ea-8adc-eaa3f62f36c5.png)
![image](https://user-images.githubusercontent.com/49730521/87540886-fe8d1980-c6bd-11ea-9489-d425eae9fc3e.png)
![image](https://user-images.githubusercontent.com/49730521/87540949-18c6f780-c6be-11ea-8354-0e6549694950.png)
![image](https://user-images.githubusercontent.com/49730521/87541013-3300d580-c6be-11ea-8a6d-33030de3dcb3.png)
