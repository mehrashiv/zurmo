# zurmo

The current code is not using docker-compose. You will need to manually start the containers and link them

## Step 1 - Create the memcached image and create a new container
docker build -t zurmo-memcached .

docker run --name zurmo-memcached -d zurmo-memcached

## Step 2 - Create the mysql image and create a new container
docker build -t zurmo-mysql .

docker run --name zurmo-mysql -v /home/zurmo/Downloads/data_docker/zurmo-mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=zurmo -e MYSQL_DATABASE=zurmo -e MYSQL_USER=zurmo -e MYSQL_PASSWORD=zurmo -d zurmo-mysql

Note: The -v flag. You can ommit "-v /home/zurmo/Downloads/data_docker/zurmo-mysql:/var/lib/mysql" it if you want to store your mysql data in the container. Else replace the left side of the colon with your path on your host

## Step 3 - Create the zurmo image and create a new container
docker build -t myzurmo .

docker run --name myzurmo --link zurmo-mysql:mysql --link zurmo-memcached -d -p 8012:80 myzurmo

## Step 4 - Configure Zurmo
* Navigate to your host IP - http://192.168.1.1:8012/zurmo
* Follow instructions to check the system
* When asked to provide database and memcached information, use the following if you cut and pasted the container names:
** Database Hostname - zurmo-mysql
** Database Port - 3306
** Database Admin Username - LEAVE BLANK
** Database Admin Password - LEAVE BLANK
** Database Name - zurmo
** Remove Existing Data - Check this box
** Database Username - zurmo
** Database Password - zurmo
** Super User Password - ANY PASSWORD YOU LIKE
** Memcache Hostname - zurmo-memcached
** Memcache Port Number - 11211
** Rest values can be default
