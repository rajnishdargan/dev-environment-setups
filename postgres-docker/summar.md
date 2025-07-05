# 📦 Docker PostgreSQL Setup Guide

A step-by-step guide to set up PostgreSQL locally using Docker and Docker Compose.  
_No need to install PostgreSQL directly on your system!_

---

## 📌 What You’ll Need:

- **Docker installed** → [Install Docker](https://docs.docker.com/get-docker/)
- **Docker Compose installed** → [Install Docker Compose](https://docs.docker.com/compose/install/)

---

## 📌 Directory Structure

Create a directory on your system:
```
postgres-docker/
├── docker-compose.yml
└── (optional) beneficiary-backend.sql → if you have a SQL file to import
```
---

## 📌 Docker Compose Configuration

Inside `postgres-docker/`, create a `docker-compose.yml` file:

```
version: '3.8'

services:
  postgres:
    image: postgres:16
    container_name: my_postgres
    restart: always
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:

```

## 📖 What this file does:
- Runs PostgreSQL 16.
- Sets default user, password, and database.
- Exposes PostgreSQL on localhost:5432.
- Creates a persistent volume pgdata to save data.

## 📌 Starting the PostgreSQL Container
Open terminal inside your postgres-docker/ directory and run:
```
docker-compose up -d
```
✔️ This will download the Postgres image, create a container, and run it in the background.

## 📌 Check Running Container
```
docker ps
```

## 📌 Connect to PostgreSQL from CLI (inside Docker)
To open PostgreSQL terminal inside the container:
```
docker exec -it my_postgres psql -U myuser
```

### Use these commands inside psql:
```
\l → List all databases
\c mydb → Connect to a database
\dt → List tables in connected DB
```

## 📌 Import a .sql File into a Database
If you have a SQL dump file (like beneficiary-backend.sql):

### 1️⃣ Copy your SQL file into the Docker container:
```
docker cp beneficiary-backend.sql my_postgres:/beneficiary-backend.sql
```

### 2️⃣ Run the SQL file inside your target DB:
```
docker exec -it my_postgres psql -U myuser -d mydb -f /beneficiary-backend.sql
```
✔️ This restores your SQL dump into mydb.

## 📌 Connect PostgreSQL to pgAdmin (GUI Tool)
Open pgAdmin installed on your system.
Create a new server with the following:
- Host: localhost
- Port: 5432
- Username: myuser
- Password: mypassword
- Access your databases and tables visually.

## 📌 Connect PostgreSQL to NestJS App
In your NestJS .env file:
```
DB_HOST=localhost
DB_PORT=5432
DB_NAME=mydb
DB_USERNAME=myuser
DB_PASSWORD=mypassword
DB_TYPE=postgres
```
✔️ Your NestJS backend will now connect to this Docker-managed PostgreSQL.

## 📌 Stopping and Removing Docker Containers
To stop the container:
```
docker-compose down
```

## To stop and remove the volume (deletes database data):
```
docker-compose down -v
```

## 📌 Useful Docker Commands
### Start container
```
docker-compose up -d
```

### Stop container
```
docker-compose down
```

### Check running containers
```
docker ps
```

### Open Postgres CLI
```
docker exec -it my_postgres psql -U myuser
```

### Copy file to container
```
docker cp beneficiary-backend.sql my_postgres:/beneficiary-backend.sql
```

### Import SQL into DB
```
docker exec -it my_postgres psql -U myuser -d mydb -f /beneficiary-backend.sql
```


## 📌 Summary
- ✔️ No native PostgreSQL installation needed.
- ✔️ Cleanly runs via Docker Compose.
- ✔️ Easy to manage via terminal and pgAdmin.
- ✔️ Persistent storage using Docker volumes.
- ✔️ Perfect for local development, demos, and testing projects like NestJS apps.
