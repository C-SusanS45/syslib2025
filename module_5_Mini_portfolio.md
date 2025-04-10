# Module 5: Mini-Portfolio Assignment
# Basic OPAC and Cataloging Module Documentation

## Introduction

An integrated library system (ILS) contains modules to help streamline library operations.  An ILS has many modules including an online public access catalog (OPAC) and a cataloging module.  The OPAC is an online database containing all materials held by a library, and library patrons can use the OPAC to search for materials in the library's catalog.  The ILS also includes a cataloging module that allows librarians to add bibliographic data to the OPAC making it available to search.  

## Relational Database Structure

In a productive ILS, the relational database associated with the OPAC would consist of many tables that are related using foreign keys and normalized to prevent redundancy. The database would store thousands of bibliographic records, and library patrons would query the data using the OPAC's user interface.  For this project, only one table called Books was created.  The books table contains the following structure:

```
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| id        | int unsigned | NO   | PRI | NULL    | auto_increment |
| author    | varchar(150) | NO   |     | NULL    |                |
| title     | varchar(150) | NO   |     | NULL    |                |
| publisher | varchar(75)  | YES  |     | NULL    |                |
| copyright | year         | NO   |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
```

A basic OPAC was created to allow users to query the books table.  A cataloging module was included to allow authorized users, such as librarians or library staff, to add bibliographical records to the underlying relational database.

## Step-by-Step Setup

This section includes step-by-step setup information along with details on how the OPAC and cataloging module work.  This is a very simple example, and a real world OPAC would have a more detailed user-friendly interface along with many more search options.  The database would be more complex and contain many more types of media, not just books.  The cataloging module would accommodate updates to a much more complex database and would include many more data quality checks. 

### OPAC

The project has a basic OPAC that includes a simple HTML form called **mylibrary.html**.  The HTML form serves as the user interface for the OPAC and includes the fields search term, start date, end date, and a search button.  When the search button is selected by the user, a PHP script called  **search.php** is executed.  When called, **search.php** does the following:

1. Gets the MySQL credentional from the login.php file using the following command 
`require_once '/var/www/login.php';`.  
2. Using the credentials, a connection to the database is established using the following command: 
`$conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);`
3. When the post method is initiated by the user from the HTML form, the following SQL statement is dynamically built and executed:  
`SELECT * FROM books WHERE (author LIKE ? OR title LIKE ? OR publisher LIKE ?) AND copyright BETWEEN ? AND ?")`.
The question marks (?) are populated with the values from the HTML form and are escaped to prevent SQL injection.  
4. If results are returned, an HTML table is built to display the results, otherwise the message **No results found** is displayed.  
5. The database connection is then closed and a link to return to the search page is displayed.

### Cataloging Module

The project has a cataloging module that is used to add bibliographical information to the OPAC database.  The cataloging module has an HTML user interface saved in file **index.html** that includes the following fields author, book title, publisher, copyright, and a submit button.  When the submit button is selected by the user, a PHP script called **insert.php**.  Both **index.html** and **insert.php** are stored in directory `/var/www/html/cataloging`.  When called, **insert.php** does the following:

1. Gets the MySQL credentionals from the login.php file using the following command 
`require_once '/var/www/login.php';`.  
2. Using the credentials, a connection to the database is established using the following command: 
`$conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);`
3. When the insert method is initiated by the user from the HTML form, the following SQL insert statement is dynamically built and executed: :  
`INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)`.
The question marks (?) are populated with the values entered on the HTML form.  
4. If the new record is successfully created, the message **New record created successfully** is displayed, otherwise an error message is displayed.  
5. The database connection is then closed and a link to **Return to Cataloging Page** or **Return to Library Home Page** is displayed.

Since the catalog module allows users to update the database, security was added.  For this exercise, we used a simple authorization mechanism provided by Apache2 called htpasswd.  Security was enabled as follows:
1. A new user called `libcat` and password was created using the following command:
`sudo htpasswd -c /etc/apache2/.htpasswd libcat`
2. Update Apache so that htpasswd will be used to control access. This is done with the following command: `sudo tilde /etc/apace2/apache2.conf` and then change the word `None` to `All` on line 172. Save and exit the editor.
3. Create a new file called `.htaccess` in the cataloging directory `/var/www/html/cataloging`.
4.  Add teh following lines to the `.htaccess` file:
```
AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```
5. Check the configuration file using `apaapachectl configtest` and restart Apache2.  The status was checked before continuing. 
6. Change the group ownership of the `/var/www/html` to `www-data` using the following command `sudo chown :www-data /var/www/html`.
7. use `setgid bit` to ensure that new files created in the `/var/www/html` directory inherit the new permissions using command ` sudo chmod -R g+s /var/www/html`.

## Documentation

To better understand the database setup and PHP, I read through the lecture notes and followed along with the lecture videos.  The explanation was clear, and the code was easy to understand.  To better understand MySQL, I researched various commands and options for creating and editing databases and table structures.  Most of my research started with a Google search.