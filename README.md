# Linux-Server-Configuration-Amazon-Lightsail-
a baseline installation of a Linux server and prepare it to host my web applications. i  secured the server from a number of attack vectors, install and configure a database server and  Apache server and deploy my Item-catalog app on it 

### Basic Info

IP Address: 3.121.53.246

PORT: 2200

SSH Key: I included the private key in the "Notes to Reviewer" section when I submitted my project.

complete url to my app :http://3.121.53.246.xip.io/catalog/

## summary of software you installed and configuration changes made

## Part 1 Secure the Server

first updated and upgrade  all my currently installed packages by running the command:

```
$ sudo apt-get update
```
```
$ sudo apt-get udgrade
```
2nd changed the SSH port  from 22 to 2200 using below  command and edit ssh port to be 2200.
```
$ sudo nano /etc/ssh/sshd_config
```
3rd configure my UFW to only allow incoming traffic from SSH 2200 and HTTP 80 and NTP 123 by the following
```
$ sudo ufw default deny incoming

$ sudo ufw  default allow outgoing

$ sudo ufw allow 2200/tcp
$ sudo ufw allow www
$ sudo ufw allow ntp
```
4th Give grader user access

creat user name grader and give him sudo access

$ sudo adduser grader
$ usermod -aG sudo grader

the creat ssh kye pair using ssh-keygen after loged to grader account  i named it udacityGrader and copied the content of privit key
to provide it to grader
no can log with privite key
```
$ ssh -i udacityGrader grader@3.121.53.246 -p 2200
```
## Part 2 Prepare to Deploy ITEM catalog project


The instance timezone was already set to UTC,

2nd 

Install Apache and the libapache2-mod-wsgi, and the python set up tools packages and then restarted the Apache service 

```
$ sudo apt-get install apache2
$ sudo apt-get install libapache2-mod-wsgi
$ sudo apt-get install python-setuptools
$ sudo service apache2 restart
```


3rd installed PostgreSQL and create user catalog 


```linux
$ sudo apt-get install postgresql

$ sudo su - postgres
postgres $ psql
postgres=# CREATE DATABASE catalog;
# CREATE USER catalog;
# ALTER ROLE catalog WITH PASSWORD 'catalog'
# GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;
```

### upload my catalog to sever using GIT and first install git 

```$ sudo apt-get install git```
Following the guidance of the Digital Ocean article linked below to deploy my app

also after finishing i found some pyton modukes need to pe instaled to the app to be run like FLASK so instle PIP and the instale the modueles as below 
```
sudo apt-get install python-pip
sudo pip install Flask
sudo pip install sqlalchemy
sudo pip install oauth2client
sudo pip install requests
```

also modify the pathunde  Authorized redirect URIs on googel API for OAUTH
to be 
	http://3.121.53.246.xip.io/login
  http://localhost:8000/gconnect
  
# How to use the app
just go to the following ling to can access the Item-Catlog App 

http://3.121.53.246.xip.io/catalog/



for referance :https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps




