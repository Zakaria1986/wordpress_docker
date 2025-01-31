# wordpress_docker

Project to get docker working with wordpress, where as I previously used MAMP to run Wordpress and Drupal

# WordPress Docker Setup

This project is a Docker-based WordPress setup with MySQL as the database.

## Getting Started

Follow these steps to set up and run the project locally:

### 1. Clone the Repository

Clone this repository to your local machine using the following command:

```bash
git clone https://github.com/yourusername/wordpress_docker.git

## Then inside the directory, create Docker compose file: docker-compose.yml then copy and paste the following settings: 

version: '3.7'

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress-container
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - ./wordpress:/var/www/html
    networks:
      - wordpress-net

  db:
    image: mysql:5.7
    container_name: wordpress-db
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
      MYSQL_ROOT_PASSWORD: rootpassword
    volumes:
      - ./call-db:/var/lib/mysql
    networks:
      - wordpress-net

networks:
  wordpress-net:
    driver: bridge
```

### This will download and install everything within the docker vertual invronment. Here are some command to inspect whats what:

Docker Commands Summary
01. Check Running Containers
To list all running containers:

```
 docker ps

```

To list all containers, including stopped ones:
```docker ps -a

```

02. Check Docker Images
To list all Docker images:
` ` ` docker images``

03. Check Logs of a Container
To view logs of a container (for example, wordpress-container):
```docker logs wordpress-container

```

04. Access a Running Container's Shell
To access the shell of a running container (for example, wordpress-container):
```docker exec -it wordpress-container /bin/bash

```

05. Access MySQL Database Inside the Container
To access MySQL in a running container (for example, wordpress-db):
```docker exec -it wordpress-db mysql -u root -p

```

This will prompt you for the MYSQL_ROOT_PASSWORD. After entering it, you'll be inside the MySQL shell.

To access a specific database inside MySQL:
```USE wordpress; 

```

06. Download Database Files to Local Environment
To copy files from a container to your local environment:
```docker cp wordpress-db:/var/lib/mysql /path/to/local/folder

```

This command will copy the entire MySQL database directory (/var/lib/mysql) from the wordpress-db container to your local machine.

07. Delete Docker Containers
To stop and remove a container:
```docker stop wordpress-container

```

```docker rm wordpress-container

```

To stop and remove the database container:
```docker stop wordpress-db

```

```docker rm wordpress-db

```

08. Delete Docker Images
To delete a Docker image:
` `  ` docker rmi wordpress:latest``

```docker rmi mysql:5.7

```

09. Delete Docker Volumes
To remove volumes (which hold persistent data, like your MySQL database):
` `  ` docker volume rm wordpress_data db_data ` ``

10. Download and Rebuild Containers
If you need to rebuild your containers with new configurations:
` `  ` docker-compose down``

` `  ` docker-compose up --build -d ` ``

This will stop and remove all containers and images, then rebuild and start them again in detached mode.
