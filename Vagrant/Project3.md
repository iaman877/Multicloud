# Intro to Centos/7, Boxes and port forwarding in Vagrant
## Centos/7
CentOS that stands for Community Enterprise Operating System is one of the Linux Distributions started by Gregory Kurtzer that provides an enterprise-class free and open-source Operating System 
## Boxes
Boxes are the package format for Vagrant environments. A box can be used by anyone on any platform that Vagrant supports to bring up an identical working environment
## port forwarding
Port forwarding, or tunneling, is the behind-the-scenes process of intercepting data traffic headed for a computer's IP/port combination and redirecting it to a different IP and/or port.
# Common Vagrant Commands for port forwording 
> ![(1)](https://user-images.githubusercontent.com/49730521/76623870-42c6ac80-655a-11ea-9e58-426734513849.png)

> ![(2)](https://user-images.githubusercontent.com/49730521/76624025-86b9b180-655a-11ea-99d5-bcc7427ef671.png)

> ![(3)](https://user-images.githubusercontent.com/49730521/76624164-c97b8980-655a-11ea-80f4-69fbd93a6d67.png)

> *uncommented or write a command : config.vm.network "forwarded_port", guest: 80, host: 8080* ( make changes as per your host machine in vagrantfile)

> ![(4)](https://user-images.githubusercontent.com/49730521/76624860-1744c180-655c-11ea-85e1-971194c3a0a6.png)

> ![(5)](https://user-images.githubusercontent.com/49730521/76625207-bff32100-655c-11ea-9902-3b9108f31fd1.PNG)

> ![(5 8)](https://user-images.githubusercontent.com/49730521/76625522-6f2ff800-655d-11ea-86b0-64ffa6640f47.PNG)

> ![(5 9)](https://user-images.githubusercontent.com/49730521/76625551-80790480-655d-11ea-8833-2f9eeb28c9a0.PNG)

## Congrats we are sucessfully access HTTP Server from  vagrant machine  
