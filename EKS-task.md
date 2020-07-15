
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

![image](https://user-images.githubusercontent.com/49730521/87513874-02597580-c697-11ea-83f7-2628408001ec.png)

Run this command > kubectl create -f efs.yml , this command will deploy pods using EFS.
```
kind: Deployment
apiVersion: apps/v1
metadata:
  name: efs-provisioner
spec:
  selector:
    matchLabels:
      app: efs-provisioner
  replicas: 1
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: efs-provisioner
    spec:
      containers:
        - name: efs-provisioner
          image: quay.io/external_storage/efs-provisioner:v0.1.0
          env:
            - name: FILE_SYSTEM_ID
              value: fs-4d92189c
            - name: AWS_REGION
              value: ap-south-1
            - name: PROVISIONER_NAME
              value: gau-prov/aws-efs
          volumeMounts:
            - name: pv-volume
              mountPath: /persistentvolumes
      volumes:
        - name: pv-volume
          nfs:
            server: fs-4d92189c.efs.ap-south-1.amazonaws.com
            path: /

```
now, create one ClusterRoleBinding using this file "role.yml".

```
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: nfs-provisioner-role-binding
subjects:
  - kind: ServiceAccount
    name: default
    namespace: wordpress-mysql
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
  ```
  
Now, create a storage using this file "storage.yml".
```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: aws-efs
provisioner: gau-prov/aws-efs
```
![image](https://user-images.githubusercontent.com/49730521/87514644-308b8500-c698-11ea-9231-401129fca692.png)

Create a PVC (Persistent volume claim) using this file :"pvc.yml"

> kubectl create -f pvc.yml

```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: efs-wordpress
  annotations:
    volume.beta.kubernetes.io/storage-class: "aws-efs"
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: efs-mysql
  annotations:
    volume.beta.kubernetes.io/storage-class: "aws-efs"
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
       
      storage: 10G
```
Now, create a secret for mysql and wordress 
![image](https://user-images.githubusercontent.com/49730521/87515627-bf4cd180-c699-11ea-8055-6a9ec89af817.png)

deploy my MySQL server

```
apiVersion: apps/v1 
kind: Deployment
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          
          claimName: efs-mysql
  ```
Allow the Mysql Services 
```
apiVersion: v1
kind: Service
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  ports:
    - port: 3306
  selector:
    app: wordpress
    tier: mysql
  
  clusterIP: None
  ```
  ![image](https://user-images.githubusercontent.com/49730521/87516354-e1931f00-c69a-11ea-9b8f-b822aec010ee.png)

Now we need to deploy wordpress and execute this file using rum " kubectl create -f wordpress.yml "  command 
```

apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: frontend
    spec:
      containers:
      - image: wordpress:4.8-apache
        name: wordpress
        env:
        - name: WORDPRESS_DB_HOST
          value: wordpress-mysql
        - name: WORDPRESS_DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        ports:
        - containerPort: 80
          name: wordpress
        volumeMounts:
        - name: wordpress-persistent-storage
          mountPath: /var/www/html
      volumes:
      - name: wordpress-persistent-storage
        persistentVolumeClaim:
          claimName: efs-wordpress
  ```

