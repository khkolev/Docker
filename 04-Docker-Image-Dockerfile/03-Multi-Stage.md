# Understanding Multi-Stage Builds in Docker

## Introduction

Multi-stage builds are a feature in Docker that allows you to create smaller, more efficient images by using multiple `FROM` statements in your Dockerfile. This method enables you to separate the build environment from the runtime environment, reducing the overall size of the final image.

## Benefits of Multi-Stage Builds

- **Reduce Image Size:** By separating the build environment from the runtime environment, you can exclude unnecessary tools and files from the final image.
- **Simplify Development:** Multi-stage builds allow you to use different base images for different stages of the build process, making it easier to manage dependencies and environments.
- **Enhance Security:** Smaller images with fewer components reduce the attack surface, improving the security of your applications.

## Creating a Multi-Stage Dockerfile

In this exercise, we will create a simple multi-stage Dockerfile for a Node.js application. The goal is to compile the application in the build stage and then create a lightweight final image containing only the runtime environment and the compiled application.

### Step 1: Setting Up Your Project

Create a new directory for your project and navigate into it:

```bash
mkdir my-nodejs-app
cd my-nodejs-app
```

Create a simple `app.js` file with the following content:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

const PORT = process.env.PORT || 3000;

server.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### Step 2: Writing the Multi-Stage Dockerfile

Create a `Dockerfile` in the project directory with the following content:

```Dockerfile
# Stage 1: Build
FROM node:14 AS builder
WORKDIR /app
COPY . .
RUN npm install

# Stage 2: Runtime
FROM node:14-alpine
WORKDIR /app
COPY --from=builder /app .
EXPOSE 3000
CMD ["node", "app.js"]
```

### Step 3: Building and Running the Docker Image

Build the Docker image with the following command:

```bash
docker build -t my-nodejs-app .
```

Run your Docker container:

```bash
docker run -p 3000:3000 my-nodejs-app
```

### Step 4: Verifying the Application

Open your web browser and navigate to `http://localhost:3000`. You should see the "Hello, World!" message.

## Implement Multi-Stage Build
### Step 1: Clone the Application
First, clone the sample application from GitHub:

```Bash
git clone https://github.com/docker/welcome-to-docker
cd welcome-to-docker
```
### Step 2: Refactor Dockerfile to Use Multi-Stage Builds
**Build Stage**
Create a new stage named `builder` to handle the installation of dependencies and building of the application.

```Dockerfile
# Build Stage
FROM node:18-alpine as builder
WORKDIR /app
COPY package*.json ./
COPY ./src ./src
COPY ./public ./public
RUN npm install && npm run build
```

**Runtime Stage**
After the build stage, define the runtime stage which will serve the built application using `serve`.

```Dockerfile
# Runtime Stage
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/build ./build
RUN npm install -g serve
EXPOSE 3000
CMD ["serve", "-s", "build"]
```

### Step 3: Build and Compare Image Sizes
Build the Docker image using the original Dockerfile and note the image size. Then, rebuild the image using your new multi-stage Dockerfile and compare the sizes.
```Bash
# Build with the original Dockerfile
docker build -t app-original .

# Build with the multi-stage Dockerfile
docker build -t app-optimized  -f Dockerfile-opt .
```
Use docker images to list the sizes of both images and observe the difference.

### Step 4: Running the Docker Images and Verifying the Applications


Run your Docker container:

```bash
docker run -d -p 3000:3000 app-original
docker run -d -p 3001:3000 app-optimized
```

### Step 5: Verifying the Application

Open your web browser and navigate to `http://localhost:3000` and  `http://localhost:3001`. 