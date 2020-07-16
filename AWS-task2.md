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
_________________________________________________________________________________________________________________
### Create a Security group with http,ssh,NFS enable 
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
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
  tags = {
    Name = "allow_HTTP"
  }
}

```
### Create is a S3 bucket with Public access policy 
```
resource "aws_s3_bucket" "bucket1" {
  bucket = "justlookingforsomeuniquenamewithoutspaces"
  force_destroy = true
  acl    = "public-read"
  policy = <<POLICY
{
  "Version": "2012-10-17",
  "Id": "MYBUCKETPOLICY",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::justlookingforsomeuniquenamewithoutspaces/*"
    }
  ]
}
POLICY 
}

```
![image](https://user-images.githubusercontent.com/49730521/87540803-e0bfb480-c6bd-11ea-8adc-eaa3f62f36c5.png)
### Upload an image in the S3 bucket 
```
resource "aws_s3_bucket_object" "object" {
  bucket = aws_s3_bucket.bucket1.id
  key    = "img1"
  source = "C:\Users\HP\Desktop\AWS-tsak2/img1.jpg"
  etag = "C:\Users\HP\Desktop\AWS-tsak2/img1.jpg"
depends_on = [aws_s3_bucket.bucket1,
		]
}
locals{
  s3_origin_id = "aws_s3_bucket.bucket1.id"
  depends_on = [aws_s3_bucket.bucket1,
		]
}
```

![image](https://user-images.githubusercontent.com/49730521/87638673-d2c36f80-c761-11ea-93f8-384bddf3c6dc.png)

### Create a EFS file system and mount with EC2 instance 

```
resource "aws_efs_file_system" "allow_nfs" {
 depends_on =  [ aws_security_group.allow_http_NFS,
                aws_instance.instance_ec2,  ] 
  creation_token = "allow_nfs"

  tags = {
    Name = "allow_nfs"
  }
}
resource "aws_efs_mount_target" "mount_target" {
 depends_on =  [ aws_efs_file_system.allow_nfs,
                         ] 
  file_system_id = aws_efs_file_system.allow_nfs.id
  subnet_id      = aws_instance.instance_ec2.subnet_id                         
  security_groups = ["${aws_security_group.allow_http_NFS.id}"]
}

```
![image](https://user-images.githubusercontent.com/49730521/87540949-18c6f780-c6be-11ea-8354-0e6549694950.png)

### Create a cloudfront for delivering the Image Content  

```
resource "null_resource" "null-remote-1"  {
 depends_on = [ 
               aws_efs_mount_target.mount_target,
                  ]
  connection {
    type     = "ssh"
    user     = "ec2-user"
    private_key = tls_private_key.private_key.private_key_pem
    host     = aws_instance.instance_ec2.public_ip
  }
  provisioner "remote-exec" {
      inline = [
        "sudo echo ${aws_efs_file_system.allow_nfs.dns_name}:/var/www/html efs defaults,_netdev 0 0 >> sudo /etc/fstab",
        "sudo mount  ${aws_efs_file_system.allow_nfs.dns_name}:/  /var/www/html",
        "sudo https://raw.githubusercontent.com/Vedanshshri/new-repo/master/web.html > index.html",                                 
        "sudo cp index.html  /var/www/html/",                  
      ]
  }
}
resource "aws_cloudfront_origin_access_identity" "o" {
     comment = "this is oai"
 }


resource "aws_cloudfront_distribution" "cloudfront1" {
  depends_on = [ 
                 aws_s3_bucket_object.object,
                  ]

  origin {
    domain_name = aws_s3_bucket.bucket1.bucket_regional_domain_name
    origin_id   = local.s3_origin_id
    s3_origin_config {
           origin_access_identity = aws_cloudfront_origin_access_identity.o.cloudfront_access_identity_path 
     }
  }

  enabled             = true
  is_ipv6_enabled     = true
  comment             = "Some comment"
  default_root_object = "terraform.png"




  logging_config {
    include_cookies = false
    bucket          =  aws_s3_bucket.bucket1.bucket_domain_name
    
  }

  default_cache_behavior {
    allowed_methods  = ["DELETE", "GET", "HEAD", "OPTIONS", "PATCH", "POST", "PUT"]
    cached_methods   = ["GET", "HEAD"]
    target_origin_id = local.s3_origin_id
    forwarded_values {
      query_string = false
      cookies {
        forward = "none"
      }
    }
    viewer_protocol_policy = "allow-all"
    min_ttl                = 0
    default_ttl            = 3600
    max_ttl                = 86400
  }

  # Cache behavior with precedence 0
  ordered_cache_behavior {
    path_pattern     = "/content/*"
    allowed_methods  = ["GET", "HEAD", "OPTIONS"]
    cached_methods   = ["GET", "HEAD", "OPTIONS"]
    target_origin_id = local.s3_origin_id




    forwarded_values {
      query_string = false
      cookies {
        forward = "none"
      }
    }

    min_ttl                = 0
    default_ttl            = 86400
    max_ttl                = 31536000
    compress               = true
    viewer_protocol_policy = "redirect-to-https"
  }
  price_class = "PriceClass_200"
  restrictions {
    geo_restriction {
      restriction_type = "whitelist"
      locations        = ["US", "IN","CA", "GB", "DE"]
    }
  }
  tags = {
    Environment = "production"
  }
  viewer_certificate {
    cloudfront_default_certificate = true
  }
}

```
Add the URL of the cloudfront to the index.html 
```
![image](https://user-images.githubusercontent.com/49730521/87541013-3300d580-c6be-11ea-8a6d-33030de3dcb3.png)
resource "null_resource" "null_resource2" {
 depends_on = [ aws_cloudfront_distribution.cloudfront1, ]
  connection {
    type     = "ssh"
    user     = "ec2-user"
    private_key = tls_private_key.private_key.private_key_pem
    host     = aws_instance.instance_ec2.public_ip
   }
   provisioner "remote-exec" {
      inline = [
      "sudo su << EOF",
      "echo \"<img src='https://${aws_cloudfront_distribution.cloudfront1.domain_name}/${aws_s3_bucket_object.object.key }'>\" >> /var/www/html/index.html",
       "EOF"
   ]
 }
}
resource "null_resource" "null_resource3" {
  depends_on = [
      null_resource.null_resource2,
   ]
   provisioner "local-exec" {
         command = "start chrome ${aws_instance.instance_ec2.public_ip}/index.html"
    }
}
```
## OUTPUT 

![image](https://user-images.githubusercontent.com/49730521/87660558-e0d2b980-c77c-11ea-8c02-374fae4c100e.png)

