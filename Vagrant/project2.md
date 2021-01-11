# Setting up the VirtualHost Configuration File with Apache
To install Apache, install the latest meta-package apache2 by running:

> sudo apt update

> sudo apt install apache2

creating a folder for our new website in /var/www/ by running

> sudo mkdir /var/www/gci/

we are directory created for our html page in it

> cd /var/www/gci

> nano index.html

Paste the your code in the index.html file:

```
<html>
<head>
  <title> C JAVA Python  </title>
</head>
<body>
  <p> Ablove language are programming languages !
</body>
</html>

```
We start this step by going into the configuration files directory:

> cd /etc/apache2/sites-available/

> sudo cp 000-default.conf gci.conf

> sudo nano gci.conf 

after excuting these command note down Servername and adminname as well 

--------------------------------------------------------------------------

Activating VirtualHost file

> sudo a2ensite gci.conf

> service apache2 reload

## congrats you are sucessfully launch Web page on  vagrant !
