# Introduction to Relational Databases (MySQL)

## Create a Database
Create a database in MySQL as root (root has the privileges to create a new database).

```
sudo mysql -u root
```

From the `mysql>` prompt create a new database called DinnerDB.

```
mysql> create database DinnerDB;
```

Grant all privileges to `opacuser`.

```
mysql> grant all privileges on DinnerDB.* to 'opacuseer'@'localhost';
```

Show all databases to ensure that DinnerDB is in the list using command `mysql> show databases;`.  The list should look like the following:

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
+--------------------+
6 rows in set (0.00 sec)
```

Enter `\q` to quit MySQL.

## Work with DinnerDB as opacuser. 

Now log in as user `opacuser`.

```
mysql -u opacuser -p
```

Once logged into MySQL as `opacuser`, ensure that the DinnerDB database is visible using command `show databases;`.  If you see the database, type `use DinnerDB;` to use the database.

Enter `ctrl l` to clear the screen.

Create two tables - Meals and Ingredients.

>[!NOTE]
>These tables are related using Meals primary key and Ingredients foreign key - meal_id. 

SQL Commands

> * INSERT - Add records to table
> * DELETE - delete records from a table
> * SELECT - Select records from the table
> * WHERE - Use where with other SQL statements to filter results.
> * ASC & DSC - Sort in ascending (ASC) order or descending (DSC) order.
> * JOIN - User join with SELECT to select data from multiple tables.
> * AS - Use as in the select statement to rename the column.
> * COUNT - Use count in the select statement to return the number of records that match.

## Manage Database

To reveiw privileges for user `opacuser`, use the following command:

```
show grants for 'opacuser'@'localhost';
```

The results will look something like this:

```
+--------------------------------------------------------------------------------+
| Grants for opacuser@localhost                                                  |
+--------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `opacuser`@`localhost`                                   |
| GRANT ALL PRIVILEGES ON `DinnerDB`.* TO `opacuser`@`localhost`                 |
| GRANT ALL PRIVILEGES ON `opacdb`.* TO `opacuser`@`localhost` WITH GRANT OPTION |
+--------------------------------------------------------------------------------+
3 rows in set (0.00 sec)
```

You can revoke all privileges from `opacuser` using the following command:

```
revoke all privileges on DinnerDB.* from 'opacuser'@'localhost';
```

To track other users, you can query table mysql.user when logged in as root.

Use the `drop database` command to delete a database.
Use the `drop user` command to delete a user.
