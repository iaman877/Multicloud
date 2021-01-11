# Day 4 Topic Covered
1. 👉What are the different types of Storage explain it || Use Case of S3 and EBS
1. 👉How to save the data by corruption or accidental delete
1. 👉How to attach extra space to an instance || How to create a partition of the drive. || How to format the partition.
## Solution 
1.  On AWS, object storage service is known as S3, block storage service is known as EBS, file storage is known as EFS.
⦿ On AWS mainly we have 3 kinds of EBS - Root, Ephemeral, EBS.
⦿ If you want to install any OS, we need partition and to create partition we need to use block device. The drive where we install our OS is known as Root.
 EBS : So doing these steps we can use EBS storage  
EBS is a regional service. It's assigned to a zone and can't attach the EBS volume into a different zone instance.

1. To save the data by corruption or accidental delete we should always EBS to store the data.
1. To create a partition of the drive following steps to follow:
```
Step 1 ->  fdisk  /dev/xvdf1 to create partition 
steps a - > follow the internel flow of fdisk
Step 2 -> mkdfs.ext4 /dev/xvdf1 to format the partition 
Step3 -> mkdir  /mydrive to create drive 
                 mount  /dev/xvdf1.
```
 To format the partition: use command mkfs as mkfs.ext4 <hard_disk>
