# How to use it ?

The docker-compose.yml file is used to build and run Dolibarr in the current workspace.
This docker image intended for developpement usage.
For production usage you should consider other contributor reference like https://hub.docker.com/r/tuxgasy/dolibarr 

First times create volume for maria db

    mkdir -p /opt/data/metabase
    
    docker volume create --driver local \
        --opt type=none \
        --opt device=/opt/data/metabase \
        --opt o=bind metabase-mariadb

Then, create a .env file all environment variables, including the root password, as follows (the password is raw after the equal sign) :

        MYSQL_ROOT_PASSWORD_METABASE=>O:x`+3>.Tq}pPM8]%O`sA@in?91`^
        
        METABASE_RESTART=always
        # For production 
        
        METABASE_RESTART=no
        # For test 
        

PLEASE, do apply secure permissions to this .env file (in **production**):

        chmod 600 .env


### Nginx configuration for production

Configure your local nginx, you can find sample nginx.conf.sample
Note : the redirect port is currently 6082 also set into docker-compose.xml
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
