#WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

I signed into my AWS free tier account that i previously created for my AWS certifactions. I launched a new EC2 instance using a t2.micro on the Ubuntu Server 20.04 LTS. I also created a new security group with inbound rules to open port 22 SSH and http 80, i then set the new security group for the instance. I then created a new Key Pair and downloaded it.

![Screenshot 2021-09-09 at 13 39 41](https://user-images.githubusercontent.com/87572884/132688867-ae2a013d-d8ec-4dee-84a8-f509353746b6.png)

I then tried to SSH to the instance from i term, but kept getting the timed out error message. until I relised i had deleted my defualt internet gateway. so i had to create another instance in a different region and ssh into that.
![Screenshot 2021-09-05 at 00 56 49](https://user-images.githubusercontent.com/87572884/132690386-deae7e18-0238-4ca6-99f6-8e38f277d284.png)
![Screenshot 2021-09-09 at 13 49 02](https://user-images.githubusercontent.com/87572884/132690468-4229e37e-6d5c-440e-8e12-2eac57a2b92b.png)

The Next step was to install package update. To do this i used the command 'sudo apt update' I folloewed this up by installing apache by running 'sudo apt install apache2'. In order to confirm Apache had been installed correctly, i used the command sudo systemctl status apache2.

![Screenshot 2021-09-07 at 22 30 00](https://user-images.githubusercontent.com/87572884/132692799-901dc72a-d5e6-49f3-bad2-98907c3f28d3.png)
![Screenshot 2021-09-07 at 22 30 11](https://user-images.githubusercontent.com/87572884/132692856-e1c3fdba-93bb-4e5d-b60b-fe79a737941c.png)

in order to confirm apache2 web server had been installed correctly i used the public IP address from the AWS EC2 instance to search. (http://<Public-IP-Address>:80)

  ![132388085-637c99e2-c56d-406e-8bd3-db646bbac7c8](https://user-images.githubusercontent.com/87572884/132696506-7f28b230-5381-4abc-9a51-a9839f060581.png)

to store and manage data for my site i then had to install a database management system. As MySQL is most commonly used within the PHP environment this was the system of choice. I ran the commands 'sudo apt install mysql-server' and a security script 'sudo mysql_secure_installation'.
  I then ran the command 'sudo mysql' to test if i was able to log on to the mysql server. 
  
  ![Screenshot 2021-09-09 at 14 46 24](https://user-images.githubusercontent.com/87572884/132697838-2d45a2ec-d049-4732-91d6-cd019dcbc7de.png)

  Once i had confirmed that it was working correctly i exited mysql using the 'exit' command. 
  
  In order to instal PHP, php-mysql and libapache2-mod-php i used the command 'sudo apt install php libapache2-mod-php php-mysql' these 3 were installed to php will process code to display dynamic content to the end user, php-mysql allows php to communicate with mysql databases, libapache2-mod-php allows apache to handle php files. 
  
  i then ran the command 'php -v' to confirm the PHP version. 
  
  I then wanted to test the LAMP setup by setting up a apache virtual host to hold the websites files and folders. 
  I first had to creat the directory projectlamp and assign ownership of it to the current user. 
  ![Screenshot 2021-09-08 at 22 09 21](https://user-images.githubusercontent.com/87572884/135008266-edc7b5d6-9fba-40b8-84b0-8fb7e7ff2ef9.png)

  I then had to use the text editor command Vi to create and open a configuaration file in apache's site available directory. In this new file i was telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. 
  
  ![Screenshot 2021-09-08 at 22 09 58](https://user-images.githubusercontent.com/87572884/135010043-e004348d-ebc5-4c47-be87-0528013be725.png)

  I then useed a2ensite command to enable the virtual host but had to disable the default website that came installed with Apache, as i was not using a custome domain name.
  I then made usre the config file didnt have syntax errors and reloaded apache to activate the new changes. 
  this produced the website 
  ![image](https://user-images.githubusercontent.com/87572884/135011291-8cc13ccc-98aa-4817-8edf-b94f7690e377.png)
  
  ENABLE PHP ON THE WEBSITE
  
  In order to change the order in which the index.php file is listed within the DirectoryIndex directive I edited the /etc/apache2/mods-enabled/dir.conf file by using the command below

sudo vim /etc/apache2/mods-enabled/dir.conf.
  
  once in the text editor i changed this DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm into this: DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
  
  once the apache2 file was reloaded and the PHP code (<?php
phpinfo();)  added inside the index.php file  the following site was produced.
  ![Screenshot 2021-09-08 at 22 07 37 (2)](https://user-images.githubusercontent.com/87572884/135012452-41678a9a-505c-4a0c-90d2-31a0652aafc8.png)

This page provides information about your server from the perspective of PHP.
  
