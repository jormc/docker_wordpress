# docker_wordpress
A simple Docker Compose file that compiles the Wordpress &amp; MySQL official Docker images for run together

### Basic & simple 
This Docker-Compose file uses the latest Wordpress and MySQL docker images versions. It has two volumes, oe for the database and one for the wordpress source code. For this case, I only want to modify the themes content, so I only have added the ***/wp-content/themes*** path

### MySQL database
These are the default configuration values (by environment vars):
- MYSQL_ROOT_PASSWORD: wordpress
- MYSQL_DATABASE: wordpress
- MYSQL_USER: wordpress
- MYSQL_PASSWORD: wordpress

And mounts its data volume over our local directory:
- ./database:/var/lib/mysql

### Wordpress

These are the default configuration values (by environment vars):
- WORDPRESS_DB_HOST: database:3306
- WORDPRESS_DB_PASSWORD: wordpress

Note the ***WORDPRESS_DB_HOST*** variable. It's very important, because if you don't define it Wordpress won't connect to MySQL host...

### Start & Test it
Starts and test with Docker-Compose, it is very simple:
```sh
$ docker-compose up
```

After Docker starts you'll find in your local folder two extra folders, that are the local volumes:

- database 
- wordpress

Enjoy!