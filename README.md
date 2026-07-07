# PHP & MySQL Fullstack Lab with Docker

A beginner-friendly guide to building a local PHP and MySQL development environment using Docker and Docker Compose on Linux Mint.

---

# Overview

This project demonstrates how to create a simple PHP development environment with MySQL using Docker. It is designed for learning full-stack web development, local server management, and containerized application deployment.

---

# 📁 Step 1: Create the Project Directory

Open your terminal and run:

```bash
mkdir ~/Desktop/php-fullstack-lab
cd ~/Desktop/php-fullstack-lab
code .
```

Visual Studio Code will open the newly created project folder.

---

# 🐳 Step 2: Create the `docker-compose.yml` File

Create a file named `docker-compose.yml` and add the following configuration:

```yaml
version: "3.8"

services:
  web:
    image: php:8.2-apache
    container_name: php_web_server
    ports:
      - "8080:80"
    volumes:
      - ./src:/var/www/html
    networks:
      - lab_network
    depends_on:
      - db

  db:
    image: mysql:5.7
    container_name: mysql_database
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: your_password
      MYSQL_DATABASE: sample_database
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - lab_network

volumes:
  db_data:

networks:
  lab_network:
    driver: bridge
```

This configuration creates:

- A PHP 8.2 + Apache web server
- A MySQL 5.7 database server
- A shared Docker network
- Persistent database storage using Docker volumes

---

# 📄 Step 3: Create the `src` Directory and `index.php`

Create a folder named `src`.

Inside it, create an `index.php` file:

```php
<?php

echo "<h1>Hello, Docker Fullstack Lab!</h1>";
echo "<p>Your PHP server is running successfully.</p>";

?>
```

---

# 🚀 Step 4: Start the Docker Containers

Inside the project directory, execute:

```bash
docker compose up -d
```

Docker will download the required images (if necessary) and start all services in the background.

---

# 🛠️ Step 5: Install Docker (If Needed)

Update your package list:

```bash
sudo apt update
```

Install Docker:

```bash
sudo apt install docker.io -y
```

Install Docker Compose:

```bash
sudo apt install docker-compose-v2 -y
```

Allow your user account to run Docker commands without `sudo`:

```bash
sudo usermod -aG docker $USER
```

After running this command, log out and log back in (or restart your system) for the changes to take effect.

---

# 🌐 Step 6: Open the Application

Launch your browser and visit:

```text
http://localhost:8080
```

If everything is configured correctly, you should see the output from `index.php`.

---

# ⚠️ Troubleshooting

## TLS Handshake Timeout

If Docker fails to download images due to a network timeout:

1. Switch to a more stable internet connection.
2. Stop and remove the running containers:

```bash
docker compose down
```

3. Restart the containers:

```bash
docker compose up -d
```

Docker will continue downloading from where it stopped instead of starting over.

---

## Port Already in Use

If port **8080** or **3306** is already occupied:

- Stop the conflicting service.
- Or change the port mapping inside `docker-compose.yml`.

Example:

```yaml
ports:
  - "8081:80"
```

---

## Verify Running Containers

To check whether your containers are running:

```bash
docker ps
```

To view logs:

```bash
docker compose logs
```

---

# Project Structure

```text
php-fullstack-lab/
├── docker-compose.yml
└── src/
    └── index.php
```

---

# Learning Objectives

By completing this lab, you will learn how to:

- Create a Docker Compose project.
- Run PHP inside a Docker container.
- Connect PHP with a MySQL database.
- Manage Docker containers.
- Build a local full-stack development environment.
- Prepare for more advanced backend development.

---

# Technologies Used

- PHP 8.2
- MySQL 5.7
- Docker
- Docker Compose
- Apache HTTP Server
- Linux Mint

---

# Conclusion

This project provides a simple and practical introduction to containerized full-stack development using Docker. It establishes a reusable development environment for PHP and MySQL applications while introducing the core concepts of Docker Compose, container networking, and persistent storage.

---

# Author

**Faris**

This repository is part of my learning portfolio for Full-Stack Web Development using Docker and Linux.
---
