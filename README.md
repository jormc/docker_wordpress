# docker_wordpress

A simple Docker Compose file that compiles the Wordpress &amp; MySQL latest official Docker images for run together.

## Basic & simple

This **Docker Compose** file uses the latest Wordpress and MySQL docker images versions. It has two volumes, one for the database and each one for the wordpress source code. 

Furthermore, in this case, I also want to have a local volume in which I can modify the website themes, so I have added the **_$PWD/wordpress/wp-content/themes_** path as a local volume. From there you can edit and make a live test of your own themes, for example.

## Services

### Wordpress

We're using the latest Wordpress docker image, without modifications. So we can pre-configure it from our docker compose file.

Its container name is **wordpress**.

#### Environment 

These are the default configuration values (by environment vars):

```
- WORDPRESS_DB_HOST=database
- WORDPRESS_DB_USER=wordpress
- WORDPRESS_DB_PASSWORD=wordpress
- WORDPRESS_DB_NAME=wordpress
```

Note the `WORDPRESS_DB_HOST` variable. It's very important, because if you don't define it Wordpress won't connect to MySQL host...

#### Volumes

By default we've created a volume, named **wp_data**, that points to the internal path `/var/www/html`, where the base html files are located.

In the other side, we can point to another path, if we need it.

At this case I've mounted the internal `/wp-content/themes` as volume under a local folder named `/wordpress/wp-content/themes` (line 10), so I'd edit wordpress themes, for example.

#### Exposed ports

Once the services are up, you can access to your Wordpress app at port 80.

### MySQL database

We're using the latest MySQL docker image for this compose.

Its container name is **database**.

#### Environment 

These are the default configuration values (by environment vars):

```
- MYSQL_DATABASE=wordpress
- MYSQL_USER=wordpress
- MYSQL_PASSWORD=wordpress
- MYSQL_ROOT_PASSWORD=12345
```

Note the default values for the database name, user, root and their passwords.

#### Volumes

The compose file mounts a database data volume named **db_volume**.

#### Exposed ports

MySQL service uses internal 3306 port that is not exposed by default for security reasons. You can access to the db content using the PHPMyAdmin service.

### PHPMyAdmin

A MySQL database administration webapp that brings to you access to the internal database content.

Its container name is **phpmyadmin**.

#### Environment 

These are the environment config params for PHPMyAdmin instance:

```
- PMA_ARBITRARY=1
- PMA_HOST=database
- PMA_USER=wordpress
- PMA_PASSWORD=wordpress
- MYSQL_ROOT_PASSWORD='12345'
```

Note that all these params are related to the MySQL config.

#### Exposed ports

Once the services are up, you can access to your PHPMyAdmin instance at port 81 (by default is 80, but we've redirected it so 80 is ccupied by Wordpress instance).

## Networking

We're using networking for easily internal access and management. Its called `wp-network`.

## Start & test it

Starts and test it with Docker Compose is very simple.

Execute:

```sh
$ docker compose up
```

Official Wordpress image exposes the 80 port by default. So, you can ccess to your http://localhost address and show what's happening...

Enjoy!

---

Changelog:

v 1.1 (2024/01/16)
- Docker compose file had been updated to the last version
- Added some more environment vars to the service images
- Added PHPMyAdmin service

v 1.0 (2016/12/12)
- Initial version, with Wordpress and MySQL services