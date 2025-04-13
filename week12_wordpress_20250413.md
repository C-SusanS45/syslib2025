## Week 12: Install WordPress Assignment 

# Prepare for Install

Update the VM using the following commands:

```
sudo apt update
sudo apt -y upgrade
sudo apt -y autoremove
sudo apt clean
```

Reboot if necessary using `sudo reboot now`.

# Install WordPress

Ensure that the required version of PHP (7.4), MySQL (8.0+), and Ubutu are installed on the VM:

```
xxxx@main-ubuntu:~$ php --version
PHP 8.1.2-1ubuntu2.21 (cli) (built: Mar 24 2025 19:04:23) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.2, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.2-1ubuntu2.21, Copyright (c), by Zend Technologies
xxxx@main-ubuntu:~$ mysql --version
mysql  Ver 8.0.41-0ubuntu0.22.04.1 for Linux on x86_64 ((Ubuntu))
xxxx@main-ubuntu:~$ cat /etc/issue.net
Ubuntu 22.04.5 LTS
```

Additional PHP modules must be installed for WordPress.  Use the following command to install them:

```
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl
```

Restart apache2 `sudo systemctl restart apache2` and MySQL `sudo systemctl restart mysql`.  Make sure both are active by checking the status with `systemctl status ...`

Be sure to install zip using the command `sudo apt install zip`.

Download and extract the WordPress installation using commands:

```
cd /var/www/html
sudo wget https://wordpress.org/latest.zip
sudo unzip latest.zip
```

> [!Tip] 
>The installation directory is found on WordPress's web site.  You get the installation link `https://wordpress.org/latest.zip` by going to `https://wordpress.org/` and selecting the "Get WordPress" button and then hover over the "Download WordPress 6.7.2" button.  The download link will appear at the bottom left corner of the browser.

A new `wordpress` directory is created in `/var/www/html` - `/var/www/html/wordpress`.  

```
drwxr-sr-x 5 root www-data     4096 Feb 11 16:11 wordpress
```

## Create Database and User

Switch to the root Linux user and login as the MySQL root user.

```
xxxx@main-ubuntu:/var/www/html$ sudo su
root@main-ubuntu:/var/www/html# mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.41-0ubuntu0.22.04.1 (Ubuntu)

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

Create a new user with the following command where 'XXXXXXXXX' is a stong password.

```
create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';
```

Create a database called wordpress `create database wordpress;`.

Grant all database privileges to the wordpress user `grant all privileges on wordpress.* to 'wordpress'@'localhost';`

Make sure the database was created using `show databases;`.
```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| DinnerDB           |
| information_schema |
| mysql              |
| opacdb             |
| performance_schema |
| sys                |
| wordpress          |
+--------------------+
7 rows in set (0.00 sec)
```

Exit MySQL using `\q`.  Then exit out of the root Linux user with `exit`.  

Switch to the wordpress directory and do the following:
1. Find the `wp-config-sample.php` file.  
2. Copy the `wp-config-sample.php` file to `wp-config.php` using `sudo cp wp-config-sample.php wp-config.php`.
3. Edit `wp-config.php` using `sudo tilde wp-config.php`.
4. Replace the database name (DB_NAME) with wordpress, database username (DB_USER) with wordpress, and the DB_PASSWORD with the password defined for DB_USER.
5. Add `define('FS_METHOD','direct');` at the end of the file.
6. Save and Exit the file.

> [!NOTE] 
> The wordpress can be accessed with the VM's public IP \wordpress.  It can be changed to another value like library using the move command.  For example:
>`sudo mv /var/www/html/wordpress /var/www/html/library`.

WordPress needs to write files to the wordpress directory `/var/www/html/wordpress`, so the permissions must be set using `sudo chown -R www-data:www-data /var/www/html/wordpress`.  This makes the owner `www-data`.  

## Install Script

In a browser on your local machine, do the following:
1. Navigate to wordpress on the VM public IP address `http://XXX.XXX.XX.XXX/wordpress`.
2. Select `English` and `Continue`.  
3. Complete the following fields: Site Title, username, password (should be unique and strong), email address, check "Discourage search engines from indexing this site".  
4. Select "Install WordPress".
5. A success page will appear.  Select "Log In".  
6. Enter the username and password created in step 3 and select "Log In".  This takes you to the admin dashboard.
7. Select Updates and apply all updates.
8. Select plugins and update the plugins and enable updates for all plugins.  

## Creating a WordPress Homepage

First create a title and tagline by selecting settings -> General 
* Update the Site Title.
* Update the Tagline.  I used a slogan genearator to create a suitable tagline.  

To create a custom site select Appearance -> Editor.  

To create posts to display on the custom site, select Posts -> Add New Post.  

## Challenges

Creating a WordPress homepage using the block editor was challenging in the begining.  It took some trial and error to figure out how to add an image and content to the page.  Google searches were very helpful and the undo button saved me many times.  