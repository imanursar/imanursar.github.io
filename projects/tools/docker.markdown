---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Docker 101
parent: Tools
permalink: /tools/docker
nav_order: 4
---

# Docker 101

tools
{: .badge .badge-pill .badge-primary }
container
{: .badge .badge-pill .badge-secondary }
Docker
{: .badge .badge-pill .badge-info }

<img src="/assets/images/tools/docker_01.webp" alt="drawing"  width="500"/>

## What Are Containers?

<p style='text-align: justify;'>
Containers are lightweight, portable, and self-sufficient software packages that bundle everything needed to run an application: code, runtime, system tools, libraries, and settings. By isolating software from its environment, containers ensure that applications run reliably across different computing environments, from development to production.

Think of a container like a shipping container in logistics. No matter what’s inside—a car, electronics, or food—the container itself fits seamlessly onto trucks, trains, and ships. Similarly, a software container can run on any system with a compatible runtime, such as Docker, without worrying about differences in operating systems or dependencies.
</p>

## What is Containerization?

<p style='text-align: justify;'>
Containerization is the process of packaging an application and its dependencies into a container, ensuring consistent and reliable deployment across various environments. This approach eliminates the "works on my machine" problem and simplifies software delivery by providing a standardized execution environment.
</p>

## What is Docker?

<p style='text-align: justify;'>
Docker is an open-source platform designed to build, deploy, and manage containerized applications efficiently. It has revolutionized software development by streamlining workflows, improving scalability, and making deployment faster and more reliable.
</p>

## How Docker Works

Docker follows a simple workflow to manage applications:
- **Build**: Developers create a `Dockerfile` to define the application’s environment and dependencies. The `docker build` command generates an image from these instructions.
- **Ship**: Built images are stored in a Docker registry (like Docker Hub or a private registry) for easy distribution.
- **Run**: Containers are instantiated from images using `docker run`, allowing applications to execute in isolated environments.

## Installing Docker

To get started with Docker, you need to install it on your system. Follow these steps based on your operating system:
  - Windows & macOS
    - Download Docker Desktop from [Docker’s official website](https://docs.docker.com/get-started/get-docker/).
    - Run the installer and follow the setup instructions.
    - Verify installation with:
    ```
    docker --version
    ```
  - Linux (Ubuntu/Debian-based)
    - Update package index and install required dependencies:
    ```
    sudo apt update
    sudo apt install ca-certificates curl gnupg
    ```
    - Add Docker’s official GPG key:
    ```
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.gpg > /dev/null
    ```
    - Set up the repository and install Docker:
    ```
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt update
    sudo apt install docker-ce docker-ce-cli containerd.io
    ```
    - Verify installation:
    ```
    docker --version
    ```

## Docker Port Mapping Explained

Port mapping in Docker is the process of mapping a port on the host machine to a port in the container. This is essential for accessing applications running inside containers from outside the Docker host.

## Dockerfile

A Dockerfile is a text file that contains a series of instructions on how to build a Docker image. Each instruction creates a layer in the image, and the layers are cached to speed up future builds.

Key Instructions in a Dockerfile
- FROM: Sets the base image for the subsequent instructions.
- WORKDIR: Sets the working directory inside the container.
- COPY: Copies files from the host system to the container.
- RUN: Executes a command in the container.
- CMD: Specifies the command to run when the container starts.
- EXPOSE: Documents which ports the container listens on.

## .dockerignore

A .dockerignore file works similarly to a .gitignore file. It specifies which files and directories should be ignored when building a Docker image. This helps in keeping the image lightweight and avoiding unnecessary files. This reduces the size of the build context and improve build times. Add node_modules, dist folders etc etc.

## Docker Tags

Docker tags convey useful information about a specific image version/variant. Tags allow you to identify and pull different versions of an image from a Docker registry. They are aliases to the ID of your image which often look like this: f1477ec11d12. It’s just a way of referring to your image. A good example is how Git tags refer to a particular commit in your history.


## Docker Volumes

Docker volumes are file systems that are mounted on Docker containers to preserve the data generated by the container. e.g. mounting the my-ts-app-data volume to the /app/data directory inside the container. Any data written to /app/data inside the container will be stored in the named volume on the host.

## Layers In Docker

So far we know that the Docker build consists of a series of ordered build instructions. Each instruction in a Dockerfile roughly translates to an layer also called as image layer. When you create a new container from an image, a new writable layer is added on top of the image layers, allowing the container to make changes without modifying the underlying image layers.

## What are Docker Layers?

- Base Layer: It is the starting point of your Docker image. It contains a operating system, such as Ubuntu, Alpine etc etc (whatever ur dockerfile specifies). This layer is immutable and serves as the foundation for subsequent layers.
- Intermediate Layers: These layers represent the instructions in your Dockerfile, such as RUN, COPY, and ADD. Each instruction creates a new layer on top of the previous ones. Intermediate layers are read-only and cached.
- Top Read/Write Layer: When you run a container from an image, Docker adds a writable layer on top of the read-only image layers. This allows the container to make changes without modifying the underlying image.
- Reusable & Shareable: Layers are cached and reusable across different images, which makes building and sharing images more efficient. If multiple images are built from the same base image or share common instructions, they can reuse the same layers, reducing storage space and speeding up image downloads and builds.
	
## How Layers are Created

Layers are created based on the instructions specified in the Dockerfile. Each instruction in the Dockerfile generates a new layer on top of the previous layers.

## Layer Caching

When we build a Docker image using a Dockerfile, Docker processes each instruction sequentially and creates a new layer for each one. If a layer of an image is unchanged, then the docker builder picks it up from the build cache. If a layer has changed since the last build, that layer, and all layers that follow it, must be rebuilt. 

## Docker Networks

Docker containers canʼt talk to each other by default. Hence docker networks allow containers to communicate with each other and the outside world. They enable isolation, security, and control over the communication between Docker containers.

## Types of Docker Networks

Docker provides several types of networks:
1. Bridge Network:
The default network type for standalone containers. Bridge networks create a software-based bridge between your host and the container. Containers connected to the network can communicate with each other, but they’re isolated from those outside the network. Each container in the network is assigned its own IP address. Because the network’s bridged to your host, containers are also able to communicate on your LAN and the internet. They will not appear as physical devices on your LAN, however.

2. Host Network:
Containers that use the host network mode share your host’s network stack without any isolation. They aren’t allocated their own IP addresses, and port binds will be published directly to your host’s network interface. This means a container process that listens on port 80 will bind to <your_host_ip>:80

3. Overlay Network:
Overlay networks are distributed networks that span multiple Docker hosts. The network allows all the containers running on any of the hosts to communicate with each other without requiring OS-level routing support. Overlay networks implement the networking for Docker Swarm clusters, but you can also use them when you’re running two separate instances of Docker Engine with containers that must directly contact each other. This allows you to build your own Swarm-like environments.

4. Macvlan Network:
Macvlan is another advanced option that allows containers to appear as physical devices on your network. It works by assigning each container in the network a unique MAC address. This network type requires you to dedicate one of your host’s physical interfaces to the virtual network. The wider network must also be appropriately configured to support the potentially large number of MAC addresses that could be created by an active Docker host running many containers.

5. ipvlan:
IPvLAN is an driver that offers precise control over the IPv4 and IPv6 addresses assigned to your containers, as well as layer 2 and 3 VLAN tagging and routing. This driver is useful when you’re integrating containerized services with an existing physical network. IPvLAN networks are assigned their own interfaces, which offers performance benefits over bridge-based networking.

6. None Network:
Containers that are isolated and do not have network interfaces.

## Docker Compose

Docker Compose is a tool that allows you to define and run multi-container Docker applications. It uses a YAML file (docker-compose.yml) to configure and orchestrate the services that make up your application, including their dependencies, networking, volumes, and other configuration settings.

## Best Practices for Docker

To maximize efficiency, security, and maintainability, follow these best practices:

- Writing a Dockerfile
  1. Use a lightweight base image (e.g., `alpine`, `python:slim`) to reduce size.
  In Docker Hub (the public Docker repository) there are several images available for download, each with different characteristics and sizes. Normally, images based on Alpine or BusyBox are extremely small in size compared to those based on other Linux distributions, such as Ubuntu. 
  2. Minimize layers by combining commands. 
  Combining multiple run commands into single RUN instruction this approach minimizes redundant layers and keeps the image cleaner. Use && to chain commands and clean up in the same layer.
    ```
    RUN apt-get update && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*
    ```
  3. Leverage `.dockerignore` to exclude unnecessary files and speed up builds.
  Dont keep any of you applications,data inside of your image this will directly add to the image size. Docker ignore similar to .gitignore. It lets you exclude specific files and directories from your final image.
  4. Use multi-stage builds to keep final images lean.
    -  Stage 1: Build Stage (as usual)
       -  we will setup working directory
       -  Install necessary build tools
       -  Copy and Install our python dependencies
       -  Copy Application code
       -  Use PyInstaller to Create a standalone executable
    
    ```
    #Stage 1: Build
    FROM python:3.9-slim AS builder

    #Install necessary build dependencies
    RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        gcc \
        && rm -rf /var/lib/apt/lists/*# Set the working directory
    WORKDIR /app# Copy the requirements file and install dependencies
    COPY requirements.txt ./
    RUN pip install --no-cache-dir -r requirements.txt# Copy the application code
    COPY . .# Compile the model (if necessary)
    RUN python compile_model.py# Install PyInstaller
    RUN pip install pyinstaller# Create a standalone executable
    RUN pyinstaller --onefile inference.py
    ```

    - Stage 2: Production Stage
      - start from a scratch image - a totally empty image
      - copy only the necessary files from Build stage
      - We set the entry-point to compiled application

    ```
    #Stage 2: Production
    FROM scratch

    # Set the working directory
    WORKDIR /app# Copy only the necessary files from the build stage
    COPY --from=builder /app/dist/inference /app/inference
    COPY --from=builder /app/model /app/model# Run the inference executable
    ENTRYPOINT ["/app/inference"]
    ```

- Managing Docker Containers
  - Use environment variables instead of hardcoding configurations.
  - Set resource limits using `--memory` and `--cpu` to prevent overuse.
  - Regularly remove unused images and containers:
  ```
  docker system prune -a
  ```
- Docker Compose Best Practices
  - Define service dependencies in `docker-compose.yml` to ensure the correct startup order.
  - Use named volumes for persistent data storage instead of bind mounts.
  - Avoid storing secrets directly in `docker-compose.yml`; use environment variables or secret management tools.

## Docker Compose: Managing Multi-Container Applications

Docker Compose is a tool that simplifies running multi-container applications. Instead of starting containers individually, you define them in a docker-compose.yml file and start everything with a single command.

### Example docker-compose.yml

```
version: '3.8'
services:
  app:
    image: my-app:latest
    ports:
      - "5000:5000"
    environment:
      - DB_HOST=db
    depends_on:
      - db
  db:
    image: postgres:latest
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
  db-data:
```

```
#control network and volumes
networks:
  counter-net:

volumes:
  counter-vol:

#contain 2 microservices (web-fe, redis)
services:
  web-fe:
    build: .                  # using dockerfile and app file in current folder
    command: python app.py    # running app
    ports:                    # mapping port, thus you need port 5001 to run this 
      - target: 8080
        published: 5001
    networks:                 # relate with network above
      - counter-net
    volumes:                  # mounting the volume at counter-vol 
      - type: volume
        source: counter-vol
        target: /app
  redis:
    image: "redis:alpine"     # pull redis image
    networks:
      counter-net:
```

```
#Version Declaration
version: '3.9'

#A service is a unit of deployment that defines which container image to use.
services:
    ts-express-app:                     ## first app
        build: .                        ## Builds the Docker image from the Dockerfile in the current directory.
            context: ./dir              ## [opt] Either a path to a directory containing a Dockerfile, or a url to a git repository.
            dockerfile: Dockerfile
    image: "express-mongo-ts-docker"    ## Names the image
    container_name: ts-express-app      ## Sets the container name
    restart: unless-stopped             ## restart policy, if stop, error code or crashed [no, always, on-failure, unless-stopped]
    ports:      ## Port mapping
        - "3000:3000"	
    environment:                        ## Sets the environment variable 
        - MONGO_URL=mongodb://mongodb:27017/ts-express-app-db
        - NODE_ENV=production           ## label env
    depends_on:                         ## Ensures the ts-express-app service starts after the mongodb service.
        - mongodb
    networks:
        - ts-app-network

    mongodb:                            ## second app
        image: mongo
        container_name: mongodb
        restart: unless-stopped
        volumes:                        ## Mounts the Docker volume my-ts-app-data to /data/db in the container
            - my-ts-app-data:/data/db
        networks:
            - ts-app-network 
        ports:
            - "27017:27017"

volumes:
  my-ts-app-data:                       ## We define what volumes we are using here in the end of our file.
 
networks:
  ts-app-network:
    driver: bridge 
```

```
#using ubuntu LTS version
FROM ubuntu:20.04 AS builder-image

#avoid stuck build due to user prompt
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install --no-install-recommends -y python3.9 python3.9-dev python3.9-venv python3-pip python3-wheel build-essential && \
	apt-get clean && rm -rf /var/lib/apt/lists/*

#create and activate virtual environment
#using final folder name to avoid path issues with packages
RUN python3.9 -m venv /home/myuser/venv
ENV PATH="/home/myuser/venv/bin:$PATH"

#install requirements
COPY requirements.txt .
RUN pip3 install --no-cache-dir wheel
RUN pip3 install --no-cache-dir -r requirements.txt

FROM ubuntu:20.04 AS runner-image
RUN apt-get update && apt-get install --no-install-recommends -y python3.9 python3-venv && \
	apt-get clean && rm -rf /var/lib/apt/lists/*

RUN useradd --create-home myuser
COPY --from=builder-image /home/myuser/venv /home/myuser/venv

USER myuser
RUN mkdir /home/myuser/code
WORKDIR /home/myuser/code
COPY . .

EXPOSE 5000

# make sure all messages always reach console
ENV PYTHONUNBUFFERED=1

# activate virtual environment
ENV VIRTUAL_ENV=/home/myuser/venv
ENV PATH="/home/myuser/venv/bin:$PATH"

# /dev/shm is mapped to shared memory and should be used for gunicorn heartbeat
# this will improve performance and avoid random freezes
CMD ["gunicorn","-b", "0.0.0.0:5000", "-w", "4", "-k", "gevent", "--worker-tmp-dir", "/dev/shm", "app:app"]
```

### Running Docker Compose
- Start services:
```
docker-compose up -d
```
- Check running containers:
```
docker ps
```
- Stop and remove containers:
```
docker-compose down
```

## Conclusion

Docker has transformed how we develop, deploy, and manage applications. By understanding key concepts like containers, Dockerfiles, volumes, networks, and best practices, you can build scalable and efficient applications. Docker Compose further simplifies multi-container orchestration, making it easier to manage complex applications.

By following these guidelines, you ensure that your Dockerized applications are reliable, secure, and optimized for production use.



## reference
- https://levelup.gitconnected.com/docker-beginner-to-expert-tutorial-68555aa3e544