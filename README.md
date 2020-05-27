# docker-drupal

## Grab Docker Images

`docker pull mariadb`

`docker pull drupal:latest`

## Run MariaDB container.
By using key v (volume) we tell Docker to create a new mount from the host where our data will be stored.

`docker run -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=drupal8 -e MYSQL_USER=drupal8 -e MYSQL_PASSWORD=drupal8 -v mariadb:/var/lib/mysql -d --name mariadb mariadb`

## Run Drupal container
With a link to just created MariaDB and the binding to port 80. The link is just a record in /etc/hosts specifying IP of the container with MariaDB in a virtual network created by Docker during its installation.

`docker run --name drupal8 --link mariadb:mysql -p 80:80 -d drupal:latest`

## Install Drupal 
Open `localhost:80` in browser. You need to specify database host as *'mysql'* instead of *'localhost'*. That’s the name of the binding we’ve created before.

## Bash into container

`docker exec -t -i <container_name> /bin/bash`

Your working Drupal site should be in /var/www/html

---

## Install Composer

`wget https://raw.githubusercontent.com/composer/getcomposer.org/4d7f8d40f9788de07c7f7b8946f340bf89535453/web/installer -O - -q | php -- --quiet`

put it in a directory that is part of your `PATH`, you can access it globally.
`mv composer.phar /usr/local/bin/composer`
