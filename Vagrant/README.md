# Vagrant
Vagrant is a tool for building and managing virtual machine environments in a single workflow, It has quickly become the ubiquitous go-to tool for local development across Mac, Windows, and Linux operating systems.

## Quick Start to Vagrant 
### Required Tools
* Virtualbox
* Vagrant
* cmder

## Steps to Up and Run Ubuntu Desktop (GUI Mode) via Vagrant
 1- Install cmder for Windows
> Download URL: https://cmder.net/

2- Install VirtualBox
> Download URL: https://www.virtualbox.org/wiki/Downloads

3- Install Vagrant
In order to eliminate compatibility issues, it is better to install Vagrant 2.2.6 version.
> Vagrant Download Link: https://www.vagrantup.com/downloads.html

## Most Common Vagrant Commands
vagrant -v : for checking version of vagrant
![Vagrant-version](https://user-images.githubusercontent.com/49730521/75887797-584c2000-5e50-11ea-9345-fa41e136e269.PNG)

cd e:\cloud\Ubuntu : for entering to the directory

![step2](https://user-images.githubusercontent.com/49730521/75888494-78c8aa00-5e51-11ea-95ee-35a879c608ee.PNG)

vagrant init ubuntu/trusty64 : through this command you can use box with Vagrant and intialize also :

![srep3](https://user-images.githubusercontent.com/49730521/75888818-fbea0000-5e51-11ea-8bc8-e0d54ae4af88.PNG)

vagrant up: download image and do rest of the settings and power-up the box
![step5](https://user-images.githubusercontent.com/49730521/75889303-b548d580-5e52-11ea-86ce-16cc2e089909.PNG)


vagrant ssh : for connecting vagrant to our virtual machine 

![Step6](https://user-images.githubusercontent.com/49730521/75889640-3c964900-5e53-11ea-8635-01b1ced83ffe.PNG)


vagrant destroy:  shutdown and delete the box
