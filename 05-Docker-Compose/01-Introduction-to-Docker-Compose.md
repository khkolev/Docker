# Docker Compose Practice Guide

## Part 1: Docker Compose Basics
### Step 1: Setting Up Your First Project

1.  Create a new directory for your project and navigate into it:
    
    ```bash
    mkdir myapp
    cd myapp
    ```
    
2.  Create a Dockerfile to define your first container. Use a text editor to create a file named `Dockerfile` with the following content:
    
    ```Dockerfile
    FROM busybox
    CMD ["/bin/sh", "-c", "echo ${MESSAGE:Default Echo}"]
    ```
    
3.  Build an image from the Dockerfile:
    
    ```bash
    docker build -t echo-box .
    ```
    
4.  Run a container using the built image:
    
    ```bash
    docker run echo-box
    docker run -e MESSAGE="Hello, world!" echo-box
    ``` 
    

### Step 2: Introduction to `docker-compose.yml`

1.  Create a `docker-compose.yml` file in your project directory:
    
    ```yaml
    version: '3'
    services:
      my-busybox-echo:
        image: echo-box
        environment:
          - MESSAGE=Hello, Docker Compose!
    ``` 
    
2.  Start your application with Docker Compose:
    
    ```bash
    docker compose up
    ``` 
    

### Step 3: Managing Your Application

-   Check the status of your running containers:
    
    ```bash
    docker compose ps
    ``` 
    
-   Stop and remove your application:
    
    ```bash
    docker compose down
    ```

## Part 2: Advanced Docker Compose with Nginx

### Step 1: Setting Up Advanced Services


1. **Create a Custom Nginx Dockerfile**:
   
   Create a new directory for your custom Nginx build and navigate into it:
   ```bash
   mkdir custom-nginx
   cd custom-nginx
   ```
   
   Create a `Dockerfile` with the following content to customize the Nginx image:
   ```Dockerfile
   FROM nginx:alpine
   COPY ./html /usr/share/nginx/html
   ```
   
   Create a simple HTML file in the `html` directory:
   ```bash
   mkdir html
   echo "<h1>Hello from Custom Nginx!</h1>" > html/index.html
   ```
   
   Navigate back to your project root directory:
   ```bash
   cd ..
   ```

2. **Prepare Shared Volume Content**:
   
   Create a directory for shared content and add an HTML file:
   ```bash
   mkdir shared-content
   echo "<h1>Hello from Shared Volume!</h1>" > shared-content/index.html
   ```

### Step 2: Configuring `docker-compose.yml`

Update your `docker-compose.yml` file to include both Nginx services, the shared volume, and custom networking:

```yaml
version: '3'
services:
  custom-nginx:
    build: ./custom-nginx
    ports:
      - "8080:80"
    volumes:
      - shared-content:/usr/share/nginx/html:ro

  official-nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - shared-content:/usr/share/nginx/html:ro

volumes:
  shared-content:

networks:
  default:
    driver: bridge
```

### Step 3: Running Your Advanced Docker Compose Setup

1. **Start Your Services**:
   
   Use Docker Compose to build and start your services:
   ```bash
   docker compose up --build
   ```
   
   This command builds the custom Nginx image and starts both Nginx services. The `--build` flag ensures that Docker Compose builds the custom image before starting the services.

2. **Verify Your Setup**:
   
   - Access the official Nginx service at `http://localhost` and you should see the "Hello from Shared Volume!" message.
   - Access the custom Nginx service at `http://localhost:8080` and you should see the "Hello from Custom Nginx!" message.

### Step 4: Managing Your Advanced Application

- **Check the Status**:
  
  To see the status of your running services:
  ```bash
  docker compose ps
  ```

- **Stop and Remove Your Services**:
  
  When you're done, you can stop and remove your services:
  ```bash
  docker compose down
  ```