# Wordpress Docker, MySQL, phpMyAdmin 

<div align="center" >
<!-- link to project -->
    <a href='-URL TO DEMO GOES HERE-'>
    <!-- link to local image -->
        <img src="https://picsum.photos/500/300" alt="" height="100%"/>
    </a>
</div>

<br />

<div align="center">
    <img src="https://img.shields.io/badge/-Wordpress-black?style=for-the-badge&logoColor=white&logo=wordpress&color=444140" alt="wordpress" />
    <img src="https://img.shields.io/badge/-Docker-black?style=for-the-badge&logoColor=white&logo=docker&color=2496ED" alt="docker" />
    <img src="https://img.shields.io/badge/-MySQL-black?style=for-the-badge&logoColor=white&logo=mysql&color=e57b16" alt="wordmysqlpress" />    
    <img src="https://img.shields.io/badge/-phpMyAdmin-black?style=for-the-badge&logoColor=white&logo=phpmyadmin&color=717cb2" alt="phpmyadmin" />
  </div>

## 📋 <a name="table">Table of Contents</a>

- 🤖 [Introduction](#introduction)
- ⚙️ [Tech Stack](#tech-stack) 
- 🔋 [Requirements](#requirements)
- 🕸️ [Code Snippet](#code-snippet)
- 🚀 [Installation](#installation)
- 📦 [Usage](#usage)
- 🛠️ [Customization](#customization)

<br />

## <a name="introduction">🤖 Introduction</a>

<h3 align="center">Wordpress Docker Container</h3>

Welcome to our containerized development environment for frontend, backend, and database applications! Whether you're working with React, Vue, Svelte, Vite, or our chosen tech stack featuring WordPress, MySQL, and phpMyAdmin, this repository has you covered.

This repository houses the code for deploying WordPress alongside MySQL and phpMyAdmin using the latest Docker features. Our Docker Compose configuration simplifies the setup process, allowing you to focus on building and testing your applications without worrying about complex infrastructure configurations.

## <a name="tech-stack">⚙️ Tech Stack</a>

- Wordpress
- Docker
- MySQL
- phpMyAdmin

## <a name="requirements">🔋 Requirements</a>

To get started with this Docker Compose setup, follow these steps:

Make sure you have the latest versions of **Docker** and **Docker Compose** installed on your machine.

## <a name="code-snippets">🕸️ Code Snippet</a>

<details>
<summary><code>wordpress-docker/compose.yaml</code></summary>

```yaml
version: '3.1'

services:

  # WordPress service
  wordpress: 
    image: wordpress  # Use the official WordPress image
    restart: always  # Always restart the container if it stops
    ports:
      - 8000:80  # Map port 8000 on host to port 80 in container
    environment:
      WORDPRESS_DB_HOST: db  # Database host name (linked service)
      WORDPRESS_DB_USER: admin  # WordPress database user
      WORDPRESS_DB_NAME: db  # WordPress database name
      WORDPRESS_DB_PASSWORD_FILE: /run/secrets/db_password  # Use secret file for password
      # WORDPRESS_DB_PASSWORD: password  # Uncomment and set a password directly (not recommended)
    volumes:
      - ./wordpress:/var/www/html  # Mount local WordPress directory to container's web root
    secrets:
      - db_password  # Use the specified secret for the WordPress database password

  # MySQL database service
  db:
    image: mysql:8.0  # Use MySQL 8.0 image
    restart: always  # Always restart the container if it stops
    environment:
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db_root_password  # Use secret file for root password
      MYSQL_DATABASE: db  # Name of the database
      MYSQL_USER: admin  # MySQL database user
      MYSQL_PASSWORD_FILE: /run/secrets/db_password  # Use secret file for database user password
      # MYSQL_PASSWORD: password  # Uncomment and set a password directly (not recommended)
      # MYSQL_ROOT_PASSWORD: password  # Uncomment and set a password directly (not recommended)
    volumes:
      - db:/var/lib/mysql  # Mount volume for database data persistence
    secrets:
      - db_root_password  # Use the specified secret for the MySQL root password
      - db_password  # Use the specified secret for the MySQL database user password

  # phpMyAdmin service
  phpmyadmin: 
    image: phpmyadmin/phpmyadmin  # Use the official phpMyAdmin image
    restart: always  # Always restart the container if it stops
    environment:
      - PMA_HOST=db  # Database host name (linked service)
      - PMA_USER=root  # phpMyAdmin user
      - PMA_PASSWORD=password  # phpMyAdmin password
    ports:
      - 8080:80  # Map port 8080 on host to port 80 in container

# Secrets definitions
secrets:
  db_password:  # Database user password secret
    file: db_password.txt  # File containing the password
  db_root_password:  # MySQL root password secret
    file: db_root_password.txt  # File containing the root password

# Volume definitions
volumes:
  wordpress:  # WordPress volume for data persistence
  db:  # MySQL database volume for data persistence

```
</details>

## Services

### WordPress
The WordPress service provides a robust content management system (CMS) for building dynamic websites and blogs. With Docker, managing WordPress becomes hassle-free, ensuring a consistent development environment across different platforms.

### MySQL
MySQL serves as the relational database management system (RDBMS) for storing WordPress data. Our Dockerized MySQL setup includes features like secrets management for secure password handling and data volume management for persistence.

### phpMyAdmin
phpMyAdmin offers a user-friendly web interface for managing MySQL databases. With our Docker Compose setup, you can easily access and interact with your MySQL databases through phpMyAdmin, streamlining database management tasks.

## <a name="installation">🚀 Installation</a>

Open a terminal and `cd` to the folder in which `docker-compose.yml` is saved and run:

```
docker-compose up
```

## <a name="usage">📦 Usage</a>

### Starting containers

You can start the containers with the `up` command in daemon mode (by adding `-d` as an argument) or by using the `start` command:

```
docker-compose start
```

### Stopping containers

```
docker-compose stop
```

### Removing containers

To stop and remove all the containers use the`down` command:

```
docker-compose down
```

Use `-v` if you need to remove the database volume which is used to persist the database:

```
docker-compose down -v
```

### phpMyAdmin

Access your WordPress site at `http://localhost:8000` and phpMyAdmin at `http://localhost:8080` in your browser.

The default username is `root`, and the password is the same as supplied in the `.env` file.

## <a name="customization">🛠️ Customization</a>

Feel free to customize the Docker Compose configuration and environment variables to suit your specific project requirements. Explore the possibilities of containerized development with Docker and elevate your web application development experience.