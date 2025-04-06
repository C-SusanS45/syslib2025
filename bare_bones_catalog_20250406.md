# Creating a Bare Bones Cataloging Module

In week 11, we created a Bare Bones Cataloging Module.  This included creating an HTML Form and a PHP Script.

## Security

Security was added to the new cataloging module using a simple Apache mechanism provided by the Apache2 server called `htpasswd`.  

A new user name `libcat` is created and given a password using the following command:

```
sudo htpasswd -c /etc/apache2/.htpasswd libcat
```

Next tell Apache that `htpasswd` will be used to control access.  This is done with the following command:

```
sudo tilde /etc/apace2/apache2.conf
```

Now change the word `None` on line 172 to `All` and save the change.

Finally change file `.htaccess` to require the authorization.  For example:

```
AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

Check the configuration file and restart Apache2.

## Permissions and Ownership

The Apache2 web server has a user account on your Linux server. The account name is www-data, and it's account details are stored in the /etc/passwd file

Use the grep command to view the details `grep "www-data" /etc/passwd"`.  Here's how to interpret the output:

Example: `accountname:x:1001:1002::/home/accountname:/bin/bash`
* Datafields are between colons `:`.
* `:x:` - x is the password
* `1001` - user id
* `1002` - gropu id
* `/home/accountname` - home directory
* `/bin/bash` -  default shell
* Just because it is a user in the system doesn't mean it is an actual user.  The service is assigned a user account.
* If the default shell is `/usr/sbin/nologon` the use is not allowed to log in.


## See the text book for sample HTML and PHP and a more detailed explanation.  

See the [Creating a Bare Bones Cataloging Module](https://cseanburns.github.io/systems-librarianship/5c-basic-opac-admin.html) lecture text to view the sample HTML Form and PHP search script.  
