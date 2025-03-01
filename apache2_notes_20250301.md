# Installing and Working with Apache

## Installing Apache

``` 
sudo apt install apache2
```

## Status

To verify that apache is running use the following command:

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

Apache should run in the background at all times.  Look for the following in the output to verify apache is running:

```
Loaded - appears on second line of output
Enabled - when the machine is started apache will be turned on automatically or "enabled on restert".
Active (running) - means apache is running right now.
Lines starting with dates - this is when the logs were updated last.
```

## Browsers

There are two browser options `w3m` and `elinks`.

The loopback IP address is the default address.  Loopback is the same as localhost.

Example:

```
w3m localhost
```

elinks does not appear to work with localhost, so it must be launched with the loopback IP.

```
elinks 127.0.0.1
```

## Finding the IP address

Use the following to get the local IP address:

```
ip a
```

The local ip will be under `<BROADCAST,MULTICAST,UP,LOWER_UP>)`

The public or external IP address can be found in the cloud console.  Use the external IP to view the index.html from an exteral browser.
