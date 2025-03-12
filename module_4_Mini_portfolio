# Module 4: Mini-Portfolio Assignment
# Server Setup Documentation

## LAMP Stack Introduction

A LAMP stack is used to build websites and web applications using open source software.  The open source software includes Linux, Apache, MySQL, and PHP.  Developers use LAMP stacks to create, host, and maintain web content.  For this project, the LAMP stack will be used to run a content management system and an integrated library systems.

## Installing the LAMP Stack

### Preparing to Install New software

Before installing new software, always check for and install new updates.  Use the following commands:

```
sudo apt update
sudo apt -y upgrade
sudo apt -y autoremove
sudo apt clean
```

If required, use the following command to reboot:

```
sudo reboot now
```
### Apache

Apache is a web server, or HTTP server.  Apache is the software that makes web sites available to web browsers.  

#### Installing Apache

To install Apache, you must first identify the package to install and verify the package using the following command:

```
apt search apache2 | head
apt show apache2
```

To install the package, use the following command:

```
sudo apt install apache2
```

#### Check the Status

To verify that Apache is running use the following command:
```
systemctl status apache2
```

The output will look something like this:

```
apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 202Y-MM-DD 16:54:07 UTC; 1min 36s ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 1832 (apache2)
      Tasks: 55 (limit: 1141)
     Memory: 5.5M
        CPU: 48ms
     CGroup: /system.slice/apache2.service
             ├─1832 /usr/sbin/apache2 -k start
             ├─1834 /usr/sbin/apache2 -k start
             └─1835 /usr/sbin/apache2 -k start

MMM DD 16:54:07 main-ubuntu systemd[1]: Starting The Apache HTTP Server...
MMM DD 16:54:07 main-ubuntu systemd[1]: Started The Apache HTTP Server.
```

Apache should always run in the background.  Look for the following in the output to verify Apache is running:

```
Loaded - appears on second line of output
Enabled - when the machine is started Apache will be turned on automatically or "enabled on restart".
Active (running) - means Apache is running right now.
Last 2 Lines starting with dates - this is when the logs were updated last.
```

#### Configuring Apache – Creating a new index.html Web Page

The default webpage for the new Apache server is index.html.  To customize the file, do the following:    

1.  Navigate to `/var/www/html` using `cd /var/www.html/`. 
2.  Backup the `index.html` file using `sudo mv index.html index.html.original`.
3.  Edit the file using `sudo tilde index.html`.
4.  Test the webpage from the VM using one of the installed web browsers.  

#### Browsers

There are two browser options for the VM: w3m and elinks.  They are installed using the following commands:
```
sudo apt install w3m
sudo apt install elinks
```

The loopback IP address is the default address. Loopback is the same as localhost.
For example:

```
w3m localhost
```

Elinks does not appear to work with localhost, so it must be launched with the loopback IP.

```
elinks 127.0.0.1
```

#### Finding the IP address

Use the following to get the local IP address:
```
ip a
```

The local ip will be under `<BROADCAST,MULTICAST,UP,LOWER_UP>`.

The public or external IP address can be found in the cloud console. Use the external IP to view the `index.html` file from an external browser.

### PHP

PHP is a server-side programming language and must be installed and configured to work with webserver software (Apache).

#### Installing PHP

Install PHP and the `libapache2-mod-php` package and restart Apache.

```
sudo apt install php libapache2-mod-php
sudo systemctl restart apache2
```

Confirm the PHP version
```
php -v
```

Restart Apache
```
Sudo systemctl restart apache2
```

Make sure Apache is active and running using the following command:

```
Systemctl status apache2
```

### Verify the installation

1.  Navigate to the web document root using `cd /var/www/html/`.
2.  Create a new file called `info.php` using `sudo tilde info.php`.
3.  Add the following to the `info.php` file using `<? php phpinfo();  ?>`. Save and close the file.
4.  Open the file using the VM’s public IP using `http://XX.XXX.XX.XX/info.php`, where `XX.XXX.XX.XX` is your server's public IP address.
5.  If the file displays correctly, delete the file to prevent exposing detailed system information using `sudo rm /var/www/html/info.php`.  

#### Configuring PHP

1.  Navigate to the `mods-enabled` directory using `cd /etc/apache2/mods-enabled/`.
2.  Make a backup copy of the `dir.conf` file using `sudo cp dir.conf dir.conf.bak`.
3.  Open the `dir.conf` file using `sudo tilde dir.conf`.
4.  Reorder the directory index (first line) in the file so that it looks like the following: `DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm` and save the changes.
5.  Check the configuration `apachectl configtest`.  Look for a `syntax ok` message.
6.  Reload the Apache configuration using `sudo systemctl reload apache2`.
7.  Restart the Apache service using `sudo systemctl restart apache2`.
8.  Check Apache’s status using `systemctl status apache2`.
9.  Navigate to the `html` directory using `cd /var/www/html/`.
10.  Create a new `index.php` file using `sudo tilde index.php`.
11.  Add HTML and PHP to the new `index.php` file and save the changes.  
12.  Test the changes by navigating to the public IP address.  

### MySQL

MySQL is an open source relational database management system.  

#### Installing MySQL

Install MySQL using the following command:

```
sudo apt install mysql-server  
```

Confirm the version number
```
mysql --version
```

Check if the server is running

```
Systemctl status mysql
```

The results will look like the sample below. Look for loaded, enabled, and active (running).

```
mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat YYYY-MM-DD HH:MM:SS UTC; 2min 27s ago
    Process: 1614 ExecStartPre=/usr/share/mysql/mysql-systemd-start pre (code=exited, status=0/SUCCESS)
   Main PID: 1622 (mysqld)
     Status: "Server is operational"
      Tasks: 37 (limit: 1141)
     Memory: 354.5M
        CPU: 1.439s
     CGroup: /system.slice/mysql.service
             └─1622 /usr/sbin/mysqld

MMM DD HH:MM:SS main-ubuntu systemd[1]: Starting MySQL Community Server...
MMM DD HH:MM:SS main-ubuntu systemd[1]: Started MySQL Community Server.
```

Next run a post installation script that performs some security checks and creates a secure baseline configuration for MySQL (answer y (yes) to prompts and set the policy to 0 or LOW).

```
Sudo mysql_secure_installation
```

Log into the database using the root user.

```
Sudo mysql -u root
```

At the MySQL prompt create a new user to avoid using root for regular tasks. Substitue `XXXXXXXXX` with a valid password.

```
mysql> create user 'opacuser'@'localhost' identified by 'XXXXXXXXX';
```

Set the character encoding to UTF-8 and grant all privileges to user `opacuser`.
```
mysql> create database opacdb default character set utf8mb4 collate utf8mb4_unicode_ci;
mysql> show databases;
mysql> grant all privileges on opacdb.* to 'opacuser'@'localhost' with grant option;
```

Create a practice database and grant all privileges to the new `opacuser`.

```
mysql> create database opacdb default character set utf8mb4 collate utf8mb4_unicode_ci;
mysql> show databases;
mysql> grant all privileges on opacdb.* to 'opacuser'@'localhost' with grant option;
```

Change the MySQL prompt to be more informative by doing the following: 
1.  Edit the `.bashrc` file from the bash shell prompt to include a more informative prompt using command `tilde .bashrc`.
2.  Scroll to the bottom of the file and add the following `export MYSQL_PS1="[\d]> "` save and exit the file.
3.  Source the file by entering `source ~/.bashrc`.
4.  Login as `opacuser` by entering the following command `mysql -u opacuser -p`.  The new command prompt will show the database currently in use, for example: `[opacdb]>`

While logged into MySQL, use SQL commands to create tables that can be quiried using PHP.  

> [!NOTE]
> Use the following command to exit MySQL `\q`. 

#### Install PHP and MySQL Support and Create a PHP Script

Connect PHP and MySQL by installing PHP support for MySQL using the following command: 

```
sudo apt install php-mysql php-mysqli
```

Restart Apache and MySQL:

```
sudo systemctl restart apache2
sudo systemctl restart mysql
```

Create a `login.php` file so PHP can be authenticated in MySQL by doing the following:
1.  Navigate to `/var/www` using `cd /var/www`. 
2.  Change the `login.php` file permissions using `sudo chmod 640 login.php`.
3.  Change the owner of `login.php` using `sudo chown :www-data login.php`.
4.  Verify the permissions using `ls -l login.php`.  The new permission should be `-rw-r-----`.
5.  Open the `login.php` file using `sudo tilde login.php`.  Add the following to the file then save and exit:
```
<?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "opacuser";
$db_password = "XXXXXXXXX";
?>
```
6.  Check the PHP syntax for the `login.php` file using `sudo php -f /var/www/login.php`.  If no errors exist, there will be no output.

Create a PHP file for the website called `opac.php` by doing the following:
1.  Navigate to `/var/www/html` using `cd /var/www/html` 
2.  Create a new file called `opac.php` using `sudo tilde opac.php`.  
3.  Add PHP and HTML to file `opac.php`.
4.   Check the PHP syntax for the `opac.php` file using ` sudo php -f /var/www/html/opac.php`.  If no errors exist, only the HTML will display.  
5.  Test the changes by viewing the public IP address using a browser on your local PC.  

>[!IMPORTANT]
> In a PHP file, dollar signs ($) are interpreted as variables even when inside double quotes (“).  To fix surround by single quotes or escape the dollar signs.
