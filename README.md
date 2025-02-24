# docker-commands
Source: https://docs.docker.com/get-started/overview/

## Several useful docker commands

Delete all images and containers
```
docker system prune -a
```

List all container (even with stopped ones)
```
docker container ls -a
```

### Example for an app architecture

```
python-docker
|____ app.py
|____ requirements.txt
|____ Dockerfile
```

### Basic steps to create a Dockerfile
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. When we tell Docker to build our image by executing the `docker build` command, Docker reads these instructions and execute them consecutively and create a Docker image as a result.

The first line to add to the Dockerfile is a `# syntax` parser directive
```
# syntax=docker/dockerfile:1
```
We recommend using `docker/dockerfile:1`, which always points to the latest release of the version 1 syntax.

Next, we need to add a line in our Dockerfile that tells Docker what base image we would like to use for our application.
```
# syntax=docker/dockerfile:1

FROM ubuntu:18.04
```
Docker images can be inherited from other images. Therefore, instead of creating our own base image, we’ll use the official ubuntu image that already has all the tools and packages that we need to run on ubuntu.

Then, we install pip3 and python-dev
```
RUN apt-get update -y && apt-get install -y python3-pip python-dev
```

When running or building, many files will be cached in `/var/lib/apt/lists/`. To delete files in cache
```
RUN rm -rf /var/lib/apt/lists/*
```
This command should be run in the last RUN command.



<!-- Normally, to run an example (Flask), we use
```
python3 -m flask run
``` -->

# Remove docker completely from your system

To completely uninstall Docker from your Ubuntu system, follow these steps:

1. **Stop and remove all Docker containers**:
   ```bash
   docker stop $(docker ps -a -q)
   docker rm $(docker ps -a -q)
   ```

2. **Remove all Docker images**:
   ```bash
   docker rmi $(docker images -a -q)
   ```

3. **Remove all Docker networks**:
   ```bash
   docker network prune
   ```

4. **Remove Docker volumes and cache**:
   ```bash
   docker system prune -a
   ```

5. **Uninstall Docker packages**:
   ```bash
   sudo apt remove docker-* --auto-remove
   ```

6. **Remove leftover Docker files**:
   ```bash
   sudo rm -rf /var/lib/docker
   sudo rm -rf /var/run/docker.sock
   ```

7. **Remove the Docker group**:
   ```bash
   sudo groupdel docker
   ```