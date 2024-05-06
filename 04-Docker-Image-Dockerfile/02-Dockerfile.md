# Docker Images and Learning Dockerfiles

## Understanding Dockerfiles

Dockerfiles are text documents that contain all the commands a user could call on the command line to assemble an image. Using Dockerfiles, you can automate the process of image creation, making it reproducible and efficient.

### Structure and Syntax

A Dockerfile consists of a set of instructions, each of which creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers that have changed are rebuilt.

### Common Instructions

- `FROM`: Sets the base image for subsequent instructions. Every Dockerfile must start with a FROM instruction.
- `RUN`: Executes any commands in a new layer on top of the current image and commits the results.
- `COPY`: Copies new files or directories from the source and adds them to the filesystem of the container at the specified path.
- `ADD`: Similar to COPY, but also supports tar extraction and remote URL handling.
- `EXPOSE`: Informs Docker that the container listens on the specified network ports at runtime.
- `CMD`: Provides defaults for an executing container. There can only be one CMD instruction in a Dockerfile.
- `ENTRYPOINT`: Configures a container that will run as an executable.

## Creating a Simple Dockerfile

Let's create a Dockerfile that sets up a basic web server using Nginx.

```Dockerfile
# Use Nginx official image as the base image
FROM nginx:latest

# Copy custom HTML file to the Nginx server
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
```

Ensure you have an `index.html` file in your build context with the content you wish to serve.

### Dockerignore File

Create a `.dockerignore` file to prevent your local modules and debug logs from being copied onto your Docker image.

```plaintext
node_modules
npm-debug.log
```

## Building Docker Images from Dockerfiles

To build a Docker image from a Dockerfile, use the `docker build` command.

```bash
docker build -t my-nginx-image .
```

- `-t my-nginx-image`: Tags your image.
- `.`: Specifies the build context to the current directory.

### Build Context

The build context is the set of files located in the specified PATH or URL. The Docker build process can access any of the files in the context.

### Tagging Images

Tagging is essential for version control and organization. Use the `-t` option to tag your images with a meaningful name and version.

### Build Arguments

Use `--build-arg` to pass variables at build time that can be accessed like environment variables in the Dockerfile.

```bash
docker build --build-arg VERSION=1.0 -t my-nginx-image .
```

This guide provides a foundational understanding of Dockerfiles, from syntax and commands to creating and building your Docker images. With practice, you'll be able to create more complex Dockerfiles for your applications.
----

# Practice Guide Tasks for Creating Docker Images and Learning Dockerfiles

This guide provides practical tasks to help you understand common Dockerfile instructions and the differences between `COPY` and `ADD`.

## Task 1: Using the FROM Instruction

**Objective:** Create a Dockerfile that uses an Ubuntu base image to create a custom image.

1. Create a new directory for your Docker project and navigate into it.
2. Create a file named `Dockerfile` without any extension.
3. Open the Dockerfile in your favorite text editor and add the following line:

```Dockerfile
FROM ubuntu:latest
```

4. Save the file. This Dockerfile now uses the latest Ubuntu image as its base.

## Task 2: Running Commands with RUN

**Objective:** Install Nginx on the Ubuntu base image using the `RUN` instruction.

1. Continue editing the same Dockerfile from Task 1.
2. Add the following lines to install Nginx:

```Dockerfile
RUN apt-get update && \
    apt-get install -y nginx
```

3. Save the Dockerfile. This will update the package lists and install Nginx when the image is built.

## Task 3: Copying Files with COPY

**Objective:** Copy a local file into your Docker image.

1. Create a simple HTML file named `index.html` in the same directory as your Dockerfile.
2. Add some HTML content to `index.html`, for example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Nginx!</title>
</head>
<body>
    <h1>Hello from Docker!</h1>
</body>
</html>
```

3. In your Dockerfile, add the following line to copy `index.html` into the Nginx directory:

```Dockerfile
COPY index.html /usr/share/nginx/html/index.html
```

4. Save the Dockerfile.

## Task 4: Understanding ADD vs COPY

**Objective:** Learn the difference between `COPY` and `ADD` by adding a local tar file and a file from a URL.

1. Create a tar file named `example.tar` containing some files or directories.
2. Modify your Dockerfile to add the following line to use `ADD`:

```Dockerfile
ADD example.tar /var/www/html
```

3. Next, to demonstrate `ADD`'s capability to handle URLs, add the following line (replace `URL` with an actual URL to a file):

```Dockerfile
ADD [URL] /var/www/html
```

4. Save the Dockerfile. `ADD` can handle tar files and URLs, unlike `COPY` which is strictly for copying local files and directories.

## Task 5: Exposing Ports with EXPOSE

**Objective:** Expose port 80 for the Nginx server.

1. In your Dockerfile, add the following line:

```Dockerfile
EXPOSE 80
```

2. Save the Dockerfile. This instruction informs Docker that the container listens on port 80.

## Task 6: Setting the Default Command with CMD

**Objective:** Specify the default command to run Nginx in the foreground.

1. Modify your Dockerfile to include the following line:

```Dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

2. Save the Dockerfile. This sets the default command to start Nginx in the foreground.

## Task 7: Configuring the Container to Run as an Executable with ENTRYPOINT

**Objective:** Use `ENTRYPOINT` to configure the container to run as an executable.

1. Replace the `CMD` instruction in your Dockerfile with the following `ENTRYPOINT`:

```Dockerfile
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

2. Optionally, you can use `CMD` to specify default arguments to `ENTRYPOINT`.

3. Save the Dockerfile. Now, your container will run as an executable that starts Nginx.

By completing these tasks, you will gain hands-on experience with key Dockerfile instructions and understand the differences between `COPY` and `ADD`.