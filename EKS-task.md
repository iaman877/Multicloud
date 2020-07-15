
# Deployment of WebApp Over AWS-EKS Cluster
![image](https://user-images.githubusercontent.com/49730521/87509576-77c14800-c68f-11ea-8136-e62ff77fc7d8.png)
## About this task :
Agenda of this task is to deploy EKS services and its use-cases on real aplication : In this task, 1st  we learn about how it configure kubernetes with AWS cloud, 2nd  we will Integrate it with EBS,EFS and ELB, 3rd launch a pod that will be Wordpress with MYSQL 4th we will work on HELM, 5th launching a prometheus server on the eks integrate  with grafana.
First, we have to create an IAM user with AdministratorAccess and uses there credentials to login in the AWSCLI 
___________________________________________________________________________________________________________
First, we have to create an IAM user with AdministratorAccess and uses there credentials to login in the AWSCLI 
![image](https://user-images.githubusercontent.com/49730521/87509774-e43c4700-c68f-11ea-8496-e1c6cecb8cc9.png)

To configure the cluster over the AWS, save the file with .yml extension
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

```
metadata:
  name: vishalcluster
  region: ap-south-1


nodeGroups:
  - name: ng-1
    instanceType: t2.micro
    desiredCapacity: 2
    ssh:
          publicKeyName: mykey11	
  - name: ng-2
    instanceType: t2.micro
    desiredCapacity: 2
    ssh:
          publicKeyName: mykey11

```

![image](https://user-images.githubusercontent.com/49730521/87511232-983ed180-c692-11ea-9179-3e1709789b53.png)

_________________________________________________________________________________________________________________
![image](https://user-images.githubusercontent.com/49730521/87511402-dfc55d80-c692-11ea-9949-f3a1cd5d672e.png)

> aws eks update-kubeconfig  --name vishalcluster

create one AWS Elastic file system

![image](https://user-images.githubusercontent.com/49730521/87512776-3d5aa980-c695-11ea-909d-459b0f812742.png)

![image](https://user-images.githubusercontent.com/49730521/87512896-6f6c0b80-c695-11ea-81ef-815a57f8c917.png)

Now we need to install Mysql on our system after installing i am going to create 3 different namespaces : MYSQL, Prometheus, Grafana. 

