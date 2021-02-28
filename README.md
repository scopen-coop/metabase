# How to use it ?

The docker-compose.yml file is used to build and run Dolibarr in the current workspace.
This docker image intended for developpement usage.
For production usage you should consider other contributor reference like https://hub.docker.com/r/tuxgasy/dolibarr 

### In case of Mysql install and running on HOST (and you want target db in it)

Just remplace docker-compose.yml by docker-compose.yml.mysqlonhost
```sh
   rm docker-compose.yml
   mv docker-compose.yml.mysqlonhost docker-compose.yml
```

create a metabase database name metabase on the host mysql server and a user metabase with grant privilige on it. The password will be put in .env file (see below chapter)

### In other case

First times create volume for maria db

    mkdir -p /opt/data/metabase
    
    docker volume create --driver local \
        --opt type=none \
        --opt device=/opt/data/metabase \
        --opt o=bind metabase-mariadb
        
create network where other container can bind to

    docker create network metabase-mariadb
    
### .env file

Then, create a .env file all environment variables, including the root password, as follows (the password is raw after the equal sign) :

In case of Mysql install and running on HOST (and you want target db in it)

if you are in case of Mysql install and running on HOST (and you want target db in it)
		MYSQL_PASSWORD_METABASE=>O:x`+3>.Tq}pPM8]%O`sA@in?91`^
else
		MYSQL_ROOT_PASSWORD_METABASE=>O:x`+3>.Tq}pPM8]%O`sA@in?91`^
        
        METABASE_RESTART=always
        # For production 
        
        METABASE_RESTART=no
        # For test 
        

PLEASE, do apply secure permissions to this .env file (in **production**):

        chmod 600 .env


### Nginx configuration for production

Configure your local nginx, you can find sample nginx.conf.sample
Note : the redirect port is currently 6082 (or 3000 in case of Mysql install and running on HOST (and you want target db in it)) set into docker-compose.xml
Do not forget to run certbot or complete nginx conf file
```sh
   certbot run --nginx --redirect -d YOUR_URL
```

### Run compose
```sh
    docker-compose up
```
**for production**
        go to https://YOUR_URL 
        
**for local test**
        go to http://0.0.0.0:6082 
