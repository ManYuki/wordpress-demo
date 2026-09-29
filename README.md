# 🐳 WordPress & MySQL Docker Compose Demo

A lightweight, production-ready blueprint for running a multi-container **WordPress** site backed by a **MySQL** database using **Docker Compose**.

---

## 🚀 Prerequisites

Before you begin, ensure you have the following installed on your machine (WSL Ubuntu is recommended for Windows users):
* Docker Desktop
* Docker Compose

---

## 🛠️ Quick Start Guide

### Step 1: Clone or Create the Project Directory
```bash
mkdir wordpress-demo && cd wordpress-demo

### Step 2: Create the `docker-compose.yml` File
```yaml
version: '3.8'

services:
  wordpress-db:
    image: mysql:8.0
    container_name: wordpress-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    volumes:
      - db_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress
    restart: always
    depends_on:
      - wordpress-db
    ports:
      - "${WORDPRESS_PORT}:80"
    environment:
      WORDPRESS_DB_HOST: wordpress-db:3306
      WORDPRESS_DB_NAME: ${MYSQL_DATABASE}
      WORDPRESS_DB_USER: ${MYSQL_USER}
      WORDPRESS_DB_PASSWORD: ${MYSQL_PASSWORD}

volumes:
  db_data:

### Step 3: How to run
 
- Create a `.env` file in the project root
- Populate this file with the variables in the `.env.example` file
- Provide appropriate value to each of these variables
- Take note of the value you provided as `WORDPRESS_PORT`
- Check that both containers are running `docker compose ps` 
- Run `docker compose up` from the project root
- Open any browser on your computer and visit `http://localhost:WORDPRESS_PORT`

## Dependencies

- Git
- Docker
- Docker Compose

## License

This repository is free to use.
