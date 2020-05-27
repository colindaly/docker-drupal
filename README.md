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

