# very-basic-apache-config
### A reference for very basic level apache setup and management on Ubuntu 16.04

##### BASIC ADD-ON PACKAGES

    apt-get install -y parallel curl num-utils whois bc 

##### RESTART APACHE

    sudo systemctl restart apache2
    
##### CHECK ERROR LOG

    cat /var/log/apache2/error.log

##### 1) You can find the apache password file here: 

    /etc/apache2/.htpasswd

##### 2) you can create new users like so: 

starting a new file: 

    htpasswd -c /usr/local/etc/apache/.htpasswd-users jsmith

file is there already: 

    htpasswd /usr/local/etc/apache/.htpasswd-users jsmith

with password read (b) from command line and using bcrypt (B)

    htpasswd -pB /usr/local/etc/apache/.htpasswd-users jsmith 4lk_fld-34gt-j4

##### 2) You can find the apache conf file here: 

    /etc/apache2/sites-available

and the file itself in my case is called: 

    000-default.conf

##### 3) to set authentication for one directory: 

        <Directory "/var/www/html/user1">
                AuthType Basic
                AuthName "Restricted Content"
                AuthUserFile /etc/apache2/.htpasswd
                Require user user1
        </Directory> 

##### 4) Setting up https using Letsencrypt

https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-16-04

##### 5) Setting permissions (in a way that allows PHP to execute things like mkdir) 

    chown -R www-data:www-data /path/to/webserver/www && chmod -R g+rw /path/to/webserver/www

##### 6) Using /etc/sudoers to manage permissions

http://askubuntu.com/questions/159007/how-do-i-run-specific-sudo-commands-without-a-password

##### How to use bcrypt in php 

http://stackoverflow.com/questions/4795385/how-do-you-use-bcrypt-for-hashing-passwords-in-php

##### Changing hostname to fully qualified domain name

    vim /etc/hostname
    
##### Stress testing Apache 

NOTE: You'll need to run this command from another server or your own machine. The machine needs to have a good internet connection. 

    for i in 2000 2050 2100 2150 2200 2250 2300 2350 2400 2450 2500 2550 2650 2700 2750 2800; do ab -kc $i -t 1 http://yourdomain.com/index.html; done
