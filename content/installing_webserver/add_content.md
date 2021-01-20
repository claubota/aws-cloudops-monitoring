---
title: "Add Content"
chapter: false
weight: 20
---

To allow ec2-user to manage files in the default root directory for your Apache web 
server, modify the ownership and permissions of the /var/www directory. In this 
tutorial, you add a group named www to your EC2 instance. Then you give that 
group ownership of the /var/www directory and add write permissions for the 
group. Any members of that group can then add, delete, and modify files for the web server.

To set file permissions for the Apache web server, add the www group to your EC2 instance 
with the following command.

```commandline
sudo groupadd www
```

Add the ec2-user user to the www group:

```commandline
sudo usermod -a -G www ec2-user
```

Log out to refresh your permissions and include the new www group.

Log back in again and verify that the www group exists with the groups command.

```commandline
groups
```

Your output looks similar to the following:

```commandline
ec2-user adm wheel systemd-journal www
```

Change the group ownership of the /var/www directory and its contents to the www group.
```commandline
sudo chgrp -R www /var/www
```

Change the directory permissions of /var/www and its subdirectories to add group write permissions and set the group ID on subdirectories created in the future.
```commandline
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} +
```


Recursively change the permissions for files in the /var/www directory and its subdirectories to add group write permissions.
```commandline
find /var/www -type f -exec sudo chmod 0664 {} +
```



Add some sample content to be served by your web server. Change directory to /var/www/html and add a file called index.html.

