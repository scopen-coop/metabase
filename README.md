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

And then, you can run :

        docker-compose up

This will run 4 container Docker : Dolibarr, MariaDB, PhpMyAdmin and Maildev.

The URL to go to the Dolibarr is :

        http://0.0.0.0

The URL to go to PhpMyAdmin is (login/password is root/root) :

        http://0.0.0.0:8080

In Dolibarr configuration Email let PHP mail function, To see all mail send by Dolibarr go to maildev

        http://0.0.0.0:6081

Setup the database connection during the installation process, please use mariadb (name of the database container) as database host.
Setup documents folder, during the installation process, to /var/documents

In A metabase container is also available

        http://0.0.0.0:6082