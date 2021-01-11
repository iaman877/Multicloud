# Day 7 topic Covered 
1. 👉 How to deploy Apache Web server on AWS cloud ?
1. 👉 What is meant by document root in Apache Web server ?
1. 👉 What is vi ? How to save file in vi ?
1. 👉 Why we never want our code+data to be stored on root device in EC2 instance ?
1. 👉 How to create an EBS volume & mount it &  How to create a partition in hard disk & how to format it ?
1. 👉 What o/p do you expect on running the command "df -h" ?
1. 👉 What is winscp ? What protocol it works on ?
1. 👉 What is Cloud front in AWS ? Why is it used ?
1. 👉 What is CDN ?
1. 👉 What do you mean by Edge locations ?
## Solution 
1. Yum command is used to install Apache Server on a Linux OS then Apache provides httpd web server which can be launched in an EC2 instance. In Linux, we use "yum install httpd" to install and "systemctl start httpd" to start the httpd
1. Every webserver have their own directory from where the data is taken. The files only in this directory are visible to the client
In apache /var/www/html is the document root
1. https://linuxize.com/post/how-to-save-file-in-vim-quit-editor/#:~:text=The%20command%20to%20save%20a,type%20%3Aw%20and%20hit%20Enter%20.&text=There%20is%20also%20an%20update,if%20there%20are%20unsaved%20changes.
1. EBS is block storage whereas the S3 is object storage. The durability of EBS is around 99.8% whereas of S3 is 99.99999% But if it is some critical data then it will be lost and would not be recovered. Hence, we do not prefer to store such data on the Root Device.
1. To mount the newly created partition we need to create a partition then format it and mount it.To create a partition we need to use cmd fdisk </dev/sdx> -df-h cmd shows all partittons https://devopscube.com/mount-ebs-volume-ec2-instance/ 
1.  df-h command is used to see all the list of folders that are mounted to various device/partition
1. WinSCP for transferring files from Windows to Linux operating system which works on SCP protocol.
1. Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
1. A CDN is a globally distributed set of servers that caches content such as videos, example CloudFront
1. A site that CloudFront uses to cache copies of your content for faster delivery to users at any location
