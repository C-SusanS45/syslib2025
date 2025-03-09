# Install and Configure MySQL

## Install MySQL Community Server Package
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

Will look like the sample below.  Look for loaded, enabled, and active (running).

```
mysql.service - MySQL Community Server
     Loaded: **loaded** (/lib/systemd/system/mysql.service; **enabled**; vendor preset: enabled)
     Active: **active (running)** since Sat YYYY-MM-DD HH:MM:SS UTC; 2min 27s ago
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

Next run a post installation script that performs some security checks and creates a secure baseline configuration for MySQL (answer y (yes) to prompts).

```
Sudo mysql_secure_installation
```

Log into the database using the root user.    

```
Sudo mysql -u root
```

At the MySQL prompt create a new user and avoid using root.  

```
mysql> create user 'opacuser'@'localhost' identified by 'XXXXXXXXX';
```

Set the character encoding to UTF-8 and grant all privileges to user opacuser.

```
mysql> create database opacdb default character set utf8mb4 collate utf8mb4_unicode_ci;
mysql> show databases;
mysql> grant all privileges on opacdb.* to 'opacuser'@'localhost' with grant option;
```

## SQL Commands

```
SELECT
ALTER
DESCRIBE
UPDATE
DELETE
```

## PHP Syntax Check

Created two PHP files.  Check syntax by doing the following:

```
sudo php -f /var/www/login.php     (should have no output)
sudo php -f /var/www/html/opac.php  (should display html only)
```

### NOTE
==In a PHP file, dollar signs ($) are interpreted as variables even when inside double quotes (“).  To fix:
Either surround by single quotes or escape the dollar signs ==

