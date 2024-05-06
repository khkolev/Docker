# Docker Images 

## Section 1: Working with Docker Hub Images
### Pulling an Image

To start working with Docker images, you first need to pull an image from Docker Hub. Let's pull the latest `nginx` image as an example:

```bash
docker pull nginx:latest
```

### Listing Images

After pulling the image, you can list all the Docker images available on your system:

```bash
docker images
```

### Inspecting an Image

To get detailed information about an image, including its layers, use the `docker inspect` command:

```bash
docker inspect nginx:latest
```

## Section 2: Creating Images from Containers

### Starting a Container

First, start a container from the `nginx` image:

```bash
docker run -d --name my-nginx nginx:latest
```

### Modifying the Container

Access the container and make some changes. For instance, create a custom `index.html` page:

```bash
docker exec -it my-nginx bash -c 'echo "<h1>Hello, Docker!</h1>" > /usr/share/nginx/html/index.html'
```

### Committing the Container to an Image

After modifying the container, commit it to create a new image:

```bash
docker commit my-nginx custom-nginx:latest
```

### Verifying the New Image

List the images again to see your new custom image:

```bash
docker images
```

## Section 3: Building Images with Dockerfile

### Creating a Dockerfile

Create a `Dockerfile` in a new directory with the following content to set up a custom Nginx server:

```Dockerfile
# Use nginx:latest as the base image
FROM nginx:latest

# Copy custom index.html into the container
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
```

Make sure you have an `index.html` file in the same directory as your Dockerfile.

### Building the Image

Navigate to the directory containing your Dockerfile and run the following command to build your Docker image:

```bash
docker build -t my-custom-nginx .
```

### Running a Container from Your Image

Run a container from your newly created image:

```bash
docker run -d -p 8080:80 my-custom-nginx
```

You can now access your custom Nginx server at `http://localhost:8080`.

## Section 4: Inspecting Image Layers

### Viewing the Layers of an Image

Docker images are made up of layers. To view the layers of your custom image, use:

```bash
docker history my-custom-nginx
```

### Inspecting a Specific Layer

To inspect a specific layer within an image, you can use the `docker inspect` command with the layer's ID:

```bash
docker inspect <layer_id>
```

## Best Practices
- **Minimal Base Images**: Start with minimal base images to keep your custom images lightweight.
- **Commit with Care**: Only commit containers as new images when necessary. Prefer Dockerfiles for reproducibility.
- **Document Changes**: Keep track of changes made within containers before committing them as images. This documentation is crucial for understanding the image's contents and for future modifications.
- **Use Tags Wisely**: Tag your images with meaningful names and versions to keep track of different iterations.
- **Security**: Regularly update your images to include security patches.