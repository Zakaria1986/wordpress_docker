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

## I have added an .env file so this might look slightly different to the actual file.

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
docker_commands_summary:
  - step: "01. Check Running Containers"
    instructions:
      - description: "To list all running containers:"
        command: "docker ps"
      - description: "To list all containers, including stopped ones:"
        command: "docker ps -a"

  - step: "02. Check Docker Images"
    instructions:
      - description: "To list all Docker images:"
        command: "docker images"

  - step: "03. Check Logs of a Container"
    instructions:
      - description: "To view logs of a container (for example, wordpress-container):"
        command: "docker logs wordpress-container"

  - step: "04. Access a Running Container's Shell"
    instructions:
      - description: "To access the shell of a running container (for example, wordpress-container):"
        command: "docker exec -it wordpress-container /bin/bash"

  - step: "05. Access MySQL Database Inside the Container"
    instructions:
      - description: "To access MySQL in a running container (for example, wordpress-db):"
        command: "docker exec -it wordpress-db mysql -u root -p"
      - description: "This will prompt you for the MYSQL_ROOT_PASSWORD. After entering it, you'll be inside the MySQL shell."
      - description: "To access a specific database inside MySQL:"
        command: "USE wordpress;"

  - step: "06. Download Database Files to Local Environment"
    instructions:
      - description: "To copy files from a container to your local environment:"
        command: "docker cp wordpress-db:/var/lib/mysql /path/to/local/folder"
      - description: "This command will copy the entire MySQL database directory (/var/lib/mysql) from the wordpress-db container to your local machine."

  - step: "07. Delete Docker Containers"
    instructions:
      - description: "To stop and remove a container:"
        command: 
          - "docker stop wordpress-container"
          - "docker rm wordpress-container"
      - description: "To stop and remove the database container:"
        command: 
          - "docker stop wordpress-db"
          - "docker rm wordpress-db"

  - step: "08. Delete Docker Images"
    instructions:
      - description: "To delete a Docker image:"
        command: 
          - "docker rmi wordpress:latest"
          - "docker rmi mysql:5.7"

  - step: "09. Delete Docker Volumes"
    instructions:
      - description: "To remove volumes (which hold persistent data, like your MySQL database):"
        command: "docker volume rm wordpress_data db_data"

  - step: "10. Download and Rebuild Containers"
    instructions:
      - description: "If you need to rebuild your containers with new configurations:"
        command: 
          - "docker-compose down"
          - "docker-compose up --build -d"
      - description: "This will stop and remove all containers and images, then rebuild and start them again in detached mode."
```
