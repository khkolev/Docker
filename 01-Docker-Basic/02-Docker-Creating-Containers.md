
## Basic Container Creation

- **View Help for `docker container run`**:
    ```bash
    docker container run --help
    ```
    Use this command to see all available options for the docker container run command.

- **Run a Simple Container**:
    ```bash
    docker container run busybox
    ```
    This command runs a new container using the busybox image. If the image is not available locally, Docker pulls it   from Docker Hub.

## Listing Containers

- **List Running Containers**:
    ```bash
    docker container ls
    ```
    Shows all currently running containers.

- **List All Containers**:
    ```bash
    docker container ls -a
    ```
    Lists all containers, including those that are stopped.

## Automatically Removing Containers

- **Run and Remove Container Automatically**:
    ```bash
    docker container run --rm busybox
    ```
    The --rm flag automatically removes the container   when it exits. This is useful for cleaning up     after short-lived tasks.

## Running Containers in Detached Mode

- **Run Container in Detached Mode**:
    ```bash
    docker container run -d nginx
    ```
    The -d flag runs the container in detached mode,    allowing it to run in the background.

## Interactive Containers

- **Run Container in Interactive Mode**:
    ```bash
    docker container run -it busybox
    ```
    The -it flags allow you to interact with the    container through a terminal session. Type exit to     leave the interactive shell.

## Cleaning Up
- **Remove All Stopped Containers**:
    ```bash
    docker container prune -f
    ```
    The docker container prune -f command removes all   stopped containers from your system without   confirmation.

## Naming Containers
- **Run Container with a Custom Name**:
    ```bash
    docker container run --name c_busybox_1 busybox
    ```
    The --name flag allows you to specify a custom  name for the container, making it easier to  identify and manage.

## Summary of Key `docker container run` Flags

`--help`: Display help for the command.

`-d`: Run container in detached mode (in the background).

`--rm`: Automatically remove the container when it exits.

`-it`: Run container in interactive mode, attaching a terminal session.

`--name`: Assign a custom name to the container.