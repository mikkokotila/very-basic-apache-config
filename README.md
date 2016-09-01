# very-basic-apache-config
### A reference for very basic level apache setup and management on Ubuntu 16.04

##### RESTART APACHE

    sudo systemctl restart apache2

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
