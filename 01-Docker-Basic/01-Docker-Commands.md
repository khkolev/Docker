# Docker Commands Practice Guide

This guide provides a comprehensive overview of various Docker commands you will use for managing Docker images and containers. Each command is explained with its purpose and usage to facilitate your independent practice.

## Docker Help Commands

- **View Docker Help**: 
  ```bash
  docker -h | more
  ```
  Use this command to display the Docker help menu, which lists available Docker commands and options. The `| more` part allows you to scroll through the information if it doesn't fit on one screen.

- **View Docker Image Commands Help**:
  ```bash
  docker image -h
  ```
  This command shows help for Docker image subcommands, such as `ls`, `pull`, and `inspect`.

## Managing Docker Images

- **List Docker Images**:
  ```bash
  docker image ls
  ```
  Lists all Docker images available on your system.

- **Pull a Docker Image**:
  ```bash
  docker image pull nginx
  ```
  Downloads the `nginx` image from Docker Hub to your local machine.

- **Inspect a Docker Image**:
  ```bash
  docker image inspect [IMAGE ID]
  ```
  Replace `[IMAGE ID]` with the actual ID of the image you want to inspect. This command displays detailed information about the image in JSON format, including environment variables.

## Managing Docker Containers

- **View Docker Container Commands Help**:
  ```bash
  docker container -h
  ```
  Displays help for Docker container subcommands.

- **List Running Containers**:
  ```bash
  docker container ls
  ```
  Shows all currently running Docker containers.

- **List All Containers**:
  ```bash
  docker container ls -a
  ```
  Lists all Docker containers, including those that are stopped.

- **Run a Docker Container**:
  - BusyBox example:
    ```bash
    docker container run busybox
    ```
    Runs a new container using the `busybox` image.
  - Nginx example with port mapping and detached mode:
    ```bash
    docker container run -P -d nginx
    ```
    Runs a new `nginx` container in detached mode (`-d`) with ports automatically mapped (`-P`).

- **Inspect a Docker Container**:
  ```bash
  docker container inspect [CONTAINER ID/NAME]
  ```
  Replace `[CONTAINER ID/NAME]` with the actual ID or name of the container. This command provides detailed information about the container.

- **Container Logs, Stats, and Processes**:
  - View logs:
    ```bash
    docker logs [CONTAINER ID/NAME]
    ```
  - View real-time stats:
    ```bash
    docker stats [CONTAINER ID/NAME]
    ```
  - View running processes:
    ```bash
    docker top [CONTAINER ID/NAME]
    ```

- **Start, Stop, and Attach to Containers**:
  - Start a container:
    ```bash
    docker start [CONTAINER ID/NAME]
    ```
  - Stop a container:
    ```bash
    docker stop [CONTAINER ID/NAME]
    ```
  - Attach to a running container:
    ```bash
    docker attach [CONTAINER ID/NAME]
    ```

- **Execute Commands in a Container**:
  - Open a bash shell:
    ```bash
    docker container exec -it [CONTAINER ID/NAME] /bin/bash
    ```
  - List files in a specific directory:
    ```bash
    docker container exec -it [CONTAINER ID/NAME] ls /usr/share/nginx/html
    ```

- **Pause and Unpause Containers**:
  - Pause processes in a container:
    ```bash
    docker container pause [CONTAINER ID/NAME]
    ```
  - Unpause processes in a container:
    ```bash
    docker container unpause [CONTAINER ID/NAME]
    ```

- **Remove Containers**:
  - Remove a specific container forcefully:
    ```bash
    docker container rm -f [CONTAINER ID/NAME]
    ```
  - Remove all stopped containers:
    ```bash
    docker container prune
    ```

Use these commands as a reference during your Docker practice sessions. Remember to replace placeholders like `[CONTAINER ID/NAME]` and `[IMAGE ID]` with actual values from your Docker environment.