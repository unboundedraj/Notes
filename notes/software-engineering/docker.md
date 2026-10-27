---
title: Docker
date: 2026-10-27
tags: [docker, containerization]
---

# Introduction:

---

**Docker** is an open-source platform that packages an application and all its dependencies **(code, runtime, libraries, configuration)** into a standardized unit called a **container**.

Containers are usually lightweight because they share the host operating system's kernel rather than each running a complete guest OS. This eliminates the classic ***"it works on my machine"*** problem by guaranteeing that software runs identically across local development, staging servers, and cloud environments.


| Concept            | Meaning                                                                                                             |
| ------------------ | ------------------------------------------------------------------------------------------------------------------- |
| **Image**          | A read-only template used to create containers. It contains the app, dependencies, and instructions for running it. |
| **Container**      | A running or stopped instance of an image.                                                                          |
| **Dockerfile**     | A text file containing instructions for building an image.                                                          |
| **Registry**       | A service for storing and sharing images, such as Docker Hub.                                                       |
| **Volume**         | Docker-managed storage used to keep data beyond a container's lifecycle.                                            |
| **Network**        | Allows containers to communicate with one another.                                                                  |
| **Docker Compose** | Defines and runs an application made of multiple services using a YAML file.                                        |


## What is Docker Image?

**Analogy:** An image is like a class or blueprint; containers are instances created from it. Teams usually share images through a registry, then run their own containers.

> Images are not necessarily tiny, and containers do use disk space. An image's read-only layers can be shared by multiple containers, while each container has its own writable layer
>
> #Just like github is the collection of all of our code, Docker hub is the place where collection of all of our docker images exists.  
> [https://hub.docker.com/u/unboundedraj](https://hub.docker.com/u/unboundedraj)

## How Docker differs from a virtual machine


| Docker container                         | Virtual machine (VM)                             |
| ---------------------------------------- | ------------------------------------------------ |
| Shares the host kernel                   | Runs a guest operating system and its own kernel |
| Usually starts quickly                   | Usually takes longer to start                    |
| Typically uses fewer resources           | Typically uses more resources                    |
| Isolates application processes and files | Virtualizes a fuller machine environment         |


***On macOS and Windows, Docker Desktop typically runs Linux containers inside a lightweight Linux VM because the host kernel is not Linux.***

## Images and image layers

A **Docker image** is built from a series of layers. Many Dockerfile instructions create layers, and image layers are read-only and can be reused across images. A container adds a writable layer on top.

This reuse can save storage and speed up builds. Changing an instruction can cause Docker to rebuild that layer and subsequent layers.

## Common Docker commands

Commands are shown in one table for quick reference. Replace placeholders such as `<container>` and `<image>` with real names or IDs.


| Command                                                           | What it does                                                                                             |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `docker --version`                                                | Displays the Docker CLI version.                                                                         |
| `docker --help`                                                   | Lists Docker commands and help.                                                                          |
| `docker login`                                                    | Signs in to a container registry.                                                                        |
| `docker logout`                                                   | Signs out of a registry.                                                                                 |
| `docker pull nginx:latest`                                        | Downloads an image from a registry.                                                                      |
| `docker images`                                                   | Lists local images.                                                                                      |
| `docker build -t myapp:1.0 .`                                     | Builds an image using the Dockerfile in the current directory.                                           |
| `docker run --name web nginx`                                     | Creates and starts a container in the foreground.                                                        |
| `docker run -d --name web nginx`                                  | Creates and starts a container in the background (detached mode).                                        |
| `docker run --name web -p 8080:80 nginx`                          | Maps host port `8080` to container port `80`. Open `http://localhost:8080` if the app serves HTTP there. |
| `docker run -d --name web -e APP_MODE=dev nginx`                  | Passes an environment variable to the container.                                                         |
| `docker run -d --name web -v my-data:/usr/share/nginx/html nginx` | Mounts a named volume at a path inside the container.                                                    |
| `docker ps`                                                       | Lists running containers.                                                                                |
| `docker ps -a`                                                    | Lists all containers, including stopped ones.                                                            |
| `docker start <container>`                                        | Starts an existing stopped container.                                                                    |
| `docker stop <container>`                                         | Stops a running container gracefully.                                                                    |
| `docker restart <container>`                                      | Restarts a container.                                                                                    |
| `docker logs <container>`                                         | Displays container logs.                                                                                 |
| `docker logs -f <container>`                                      | Follows logs as new output arrives.                                                                      |
| `docker exec -it <container> sh`                                  | Opens an interactive shell in a running container (if `sh` exists).                                      |
| `docker inspect <container>`                                      | Shows detailed container or image metadata.                                                              |
| `docker rm <container>`                                           | Removes a stopped container.                                                                             |
| `docker rm -f <container>`                                        | Force-removes a container, including if running.                                                         |
| `docker rmi <image>`                                              | Removes a local image if it is not in use.                                                               |
| `docker volume create my-data`                                    | Creates a named volume.                                                                                  |
| `docker volume ls`                                                | Lists volumes.                                                                                           |
| `docker volume inspect my-data`                                   | Shows volume details.                                                                                    |
| `docker volume prune`                                             | Removes unused local volumes; review the prompt carefully.                                               |
| `docker network ls`                                               | Lists Docker networks.                                                                                   |
| `docker network create app-net`                                   | Creates a network.                                                                                       |
| `docker network inspect app-net`                                  | Shows network details.                                                                                   |
| `docker network rm app-net`                                       | Removes a network if it is not in use.                                                                   |
| `docker compose up -d`                                            | Creates/starts services defined in the Compose file in the background.                                   |
| `docker compose up --build -d`                                    | Builds/rebuilds images if needed, then starts services.                                                  |
| `docker compose ps`                                               | Lists services/containers in the Compose project.                                                        |
| `docker compose logs -f`                                          | Follows logs from Compose services.                                                                      |
| `docker compose down`                                             | Stops and removes Compose containers and project networks. Named volumes are kept unless `-v` is added.  |
| `docker compose down -v`                                          | Also removes Compose-managed named and anonymous volumes; use carefully.                                 |


### Important command details

- `docker run` **creates a new container** from an image and starts it. Running it again usually creates another container.
- `docker start` starts an **existing** container.
- Detached mode (`-d`) runs the container in the background.
- In `-p 8080:80`, the **left side is the host port** and the **right side is the container port**. A host port generally cannot be bound by two services at the same time on the same address/protocol.
- `docker exec -it <container> bash` works only if Bash is installed; `sh` is available in many smaller images.
- Be cautious with `docker system prune`, `docker volume prune`, and `docker compose down -v`: they can delete data or resources you still need.

## Ports, networks, and volumes

### Port mapping

A container port is not automatically exposed on your host. Use `-p HOST_PORT:CONTAINER_PORT` to publish it.

Example: `docker run -d --name web -p 8080:80 nginx`

- Host: `localhost:8080`
- Container: port `80`

### Networks

Containers attached to the same user-defined Docker network can usually reach each other by container name or Compose service name. In Compose, services on the default project network can use names such as `db` to connect to the database.

### Volumes

A container's writable layer is not intended as durable storage. Use a **volume** for data that must survive container replacement, such as database files.

- Named volume: `my-data:/app/data`
- Bind mount: `./local-folder:/app/data` (uses a path from your machine)

The left side of a named-volume mount is the volume name; for a bind mount, it is a host path. The right side is the path inside the container.

Volumes can be shared by containers, but concurrent access must be safe for the application. A volume is not automatically a backup.

## Dockerizing an application with a Dockerfile

A **Dockerfile** describes how to build an image. Example for a simple Node.js app:

```yaml
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

Build it from the directory containing the Dockerfile:

```
docker build -t myapp:1.0 .
```

`EXPOSE` documents the container port; it does not publish the port to the host by itself. Use `-p` or Compose `ports` to publish it.

A `.dockerignore` file helps prevent unnecessary files from entering the build context. Example:

```
node_modules
.git
.env
npm-debug.log
```

## Docker Compose

**Docker Compose** lets you define multiple services in one YAML file, such as an API, database, and cache. It can create containers, networks, and volumes for the application together.

### Example: Node.js app + Redis

This example assumes a Node.js project has a `Dockerfile`, `package.json`, and an application that listens on port `3000`. The app should read `REDIS_HOST` and `REDIS_PORT` to connect to Redis. Redis is not published to the host in this example.

Create `compose.yaml`:

```
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      REDIS_HOST: redis
      REDIS_PORT: "6379"
    depends_on:
      redis:
        condition: service_healthy

  redis:
    image: redis:7-alpine
    command: ["redis-server", "--appendonly", "yes"]
    volumes:
      - redis-data:/data
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      timeout: 3s
      retries: 5

volumes:
  redis-data:
```

Run these commands from the directory containing `compose.yaml`:

```
docker compose up --build -d
docker compose ps
docker compose logs -f app
docker compose down
```

- `app` is built from the local Dockerfile.
- `redis` is the Compose service name; the app can use `redis:6379` as the Redis address from inside the Compose network.
- `redis-data` keeps Redis data across normal container replacement and `docker compose down`.
- `depends_on` with `service_healthy` waits for Redis's health check before starting the app, but the application should still handle reconnects if Redis becomes unavailable later.
- `docker compose down -v` removes the named volume too, so avoid it if you want to keep Redis data.

For local development, use a suitable `.dockerignore` file and avoid exposing database/cache ports publicly unless needed.

## 8. Quick mental model

1. Write application code.
2. Write a `Dockerfile` to describe how to build its image.
3. Build the image with `docker build`.
4. Run a container with `docker run`, or define the application stack in `compose.yaml`.
5. Use ports for host access, networks for service-to-service communication, and volumes for persistent data.
6. Share images through a registry such as Docker Hub; teammates can pull the image and create their own containers.

## Docker in Cloud Deployment (E-commerce Example)

### 1. Dockerfile

- A Dockerfile has no extension. Its name is simply `Dockerfile`.
- It contains instructions to build a Docker image.

### 2. How cloud deployment works

For a Next.js e-commerce app, we might use:

- Next.js: Frontend and application logic.
- MongoDB: Main database for users, products, and orders.
- Redis: Fast storage for caching, sessions, etc.

These can run as separate services.

### 3. Where is the data stored?

There are two ways to run databases:

A. Self-hosted database in a Docker container

- MongoDB/Redis runs inside a container on your machine or cloud server.
- Data is stored in the container's writable filesystem by default.
- Use Docker volumes to preserve data beyond container removal.

```
docker volume create mongo-data
docker run -d --name mongodb -v mongo-data:/data/db mongo:8
```

B. Managed cloud database (e.g., MongoDB Atlas)

- MongoDB runs on infrastructure managed by the cloud provider.
- Your Next.js container connects to it using a connection string.
- Data is stored on the provider's database infrastructure, not inside your application container.
- You do not need to run MongoDB in Docker.

### 4. Typical production architecture

```
Customer
   |
   v
Next.js Docker Container
   |
   |------> MongoDB Atlas (main database)
   |
   └------> Managed Redis (cache)
```

### 5. Important points to remember


| Term           | Meaning                                    |
| -------------- | ------------------------------------------ |
| Docker image   | Packaged application                       |
| Container      | Running instance of an image               |
| Docker volume  | Persistent storage associated with Docker  |
| MongoDB Atlas  | Managed cloud database                     |
| Docker Compose | Runs multiple services together            |
| Cloud hosting  | Infrastructure where your application runs |


Key takeaway: Docker packages and runs your application; it does not require your database to run inside Docker. You can deploy your Next.js app in a container and connect it to separately managed MongoDB and Redis services.
