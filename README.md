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
