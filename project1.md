# Getting Started with Vagrant using putty
## To get started, go ahead and install these core tools:

* VirtualBox :  the software that creates virtual machines
* Vagrant : our hero, the software that deploys virtual machines and runs provisioning scripts
* PuTTY and PuTTYGen : SSH client and a generator for security keys

### note : before going to ahead you must ensure that vagrant should be up 

## Step 1 :-
### Open Putty Generator for generating Private Keys
* generate  priavte key
> go to *load* -> E:\cloud\Ubuntu\.vagrant\machines\default\virtualbox -> click private_key -> click yes -> save at any location

![puttyzen](https://user-images.githubusercontent.com/49730521/76108748-26c68680-6001-11ea-9c14-5fbd1b6f2108.PNG)

## Step 2 :-
### open  putty configuration 
go to Session

![Host](https://user-images.githubusercontent.com/49730521/76110274-3f846b80-6004-11ea-943a-44dfb9180dfb.PNG)

## Step 3 :-
go to Data

![Datae](https://user-images.githubusercontent.com/49730521/76110592-c3d6ee80-6004-11ea-999a-024184c90096.PNG)

## Step 4 :-
go to connection -> ssh -> Auth -> Browse the private file

![Authe](https://user-images.githubusercontent.com/49730521/76110784-27611c00-6005-11ea-90fa-0e2bcf57da29.PNG)

## Step 5 :-
Again go to session 

![vegrantvm](https://user-images.githubusercontent.com/49730521/76110995-832ba500-6005-11ea-92bb-2ba46da0a98a.PNG)

## Step 6 :-
and then click to open -> yes

![running](https://user-images.githubusercontent.com/49730521/76111744-d7835480-6006-11ea-8dde-557d81544024.PNG)



## congrats you are sucessfully launch Linux os  via vagrant with putty !!
