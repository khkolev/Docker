# Docker Storage: Bind Mounts
## Introduction to Bind Mounts
Bind mounts in Docker are an essential feature for developers, allowing the direct mapping of files and directories from the host to the container. This guide aims to provide students with a clear understanding of how to use bind mounts effectively, enhancing their Docker workflows.


## Getting Started with Bind Mounts
### Preparing Your Environment
First, ensure you have Docker installed on your system and that it's running. Then, create a directory on your host that you'll use for the bind mount:
```bash
mkdir ~/docker-bind-mounts/example
```

### Launching a Container with a Bind Mount
To demonstrate the power of bind mounts, we'll run a container that serves a static website using nginx, with the website files located on the host.

1. Create a simple HTML file in the directory you just made:

```bash
echo "<h1>Hello, Docker Bind Mounts!</h1>" > ~/docker-bind-mounts/example/index.html
```

2. Run an nginx container with a bind mount to serve this HTML file:

```bash
docker container run -d --name nginx-example -p 8080:80 --mount type=bind,source="$(pwd)"/example,target=/usr/share/nginx/html nginx
```

This command breaks down as follows:
- `-d` runs the container in detached mode.
- `--name nginx-example` names the container for easier reference.
- `-p 8080:80` maps port 8080 on the host to port 80 in the container, where nginx serves content by default.
- `--mount type=bind,source="$(pwd)"/example,target=/usr/share/nginx/html` creates the bind mount.

### Verifying the Bind Mount
After starting the container, navigate to `http://localhost:8080` in your web browser. You should see the message "Hello, Docker Bind Mounts!" displayed, served directly from the bind-mounted directory.

## Interacting with Bind Mounts

### Modifying Files

Any changes you make to the files in the `~/docker-bind-mounts/example` directory on the host will be immediately reflected in the container. Try editing the `index.html` file to change the message, and refresh your browser to see the update.

### Exploring the Container's Filesystem

To see how the bind mount appears from within the container, use the following command to access the container's shell:

```bash
docker container exec -it nginx-example /bin/bash
```

Navigate to the `/usr/share/nginx/html` directory and list the contents. You'll see the `index.html` file you created on the host.

## Best Practices for Using Bind Mounts
- **Security**: Be cautious with bind mounts, as they can expose your host's filesystem to the container. Only bind mount directories that the container needs to access.
- **Data Persistence**: Remember that changes made in the bind-mounted directory are reflected on both the host and the container. This is great for development but requires careful handling to avoid unintended data loss.
- **Use in Development**: Bind mounts are most beneficial in development environments, where you need to quickly test changes without rebuilding a container. For production environments, consider using Docker volumes for better encapsulation and control.

