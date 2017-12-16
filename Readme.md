#Welcome to **coreucb**.

###What is **coreucb**?
**coreucb** is nothing more then the essentials one would need to begin a UCB core Drupal 8 project. Out of the box it comes with.

* Drupal 8.1  (This is the current unofficially approved version)
* Mariadb (latest version)
* Adminer (latest version)

We currently have plans to also include.

* Redis 
* solr
* portainer

These have not yet been included as they have yet been proposed to stakeholders.

##Updating docker-compose to point at our registry.

###**Prerequisites**
* Have installed on machine docker-for-mac or docker-for-windows.  Use official download at https://www.docker.com/docker-windows
* Have installed on machine docker-toolbox.  Use official documentation on installing for your windows or mac machine located at https://github.com/docker/toolbox
* You have installed composer globally on your machine.
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');
mv composer.phar /usr/local/bin/composer"
```
> ===hit enter one last time to make sure last command fired===

> Note: If the above fails due to permissions, you may need to run it again with sudo.
Note: On some versions of OSX the /usr directory does not exist by default. If you receive the error "/usr/local/bin/composer: No such file or directory" then you must create the directory manually before proceeding: mkdir -p /usr/local/bin.

* You have installed drush on your machine.  Please use the offcial installation documentation from here. http://docs.drush.org/en/8.x/install-alternative/ 


###Installation

This is dependent on you having configured the prerequisites first.
`composer install'`
`docker-compose up --build -d`

That's it!  You can now go to http://localhost:8080/core/install.php and configure site. 

###Configuring site to communicate with database.
This will soon be automated in a make file but for now you'll want to firgure out what the host for your database is within docker. To do that follow by running these commands.

`docker ps`

copy and paste the *mariadb container id*.  It's going to appear to be a hash.  Then

`docker inspect {containerid}`

Use `cmd + f` to do a search of the output for `hostname`.  It's literal.  Copy the host name and use that and only that as the hostname value under "advance settings" on the drupal setup.  

###Accessing the container
 `bash -c "clear && docker exec -it html_drupal_1 sh`
 if html_drupal_1 doesn't work then use the name of the container.  You can obtain the name of the container by running.  `docker ps`.
 
 ###What's next?
 Well we've mounted to volumes to your computer that will serve as your themes, modules and profiles directories. 
 
Checkout the demomodule to learn how to use and build modules within our system.  Please follow the coding standards while having fun coding.

