## Docker Compose Homework Tasks

### Task 1: Create a Basic Docker Compose File
Create a `docker-compose.yml` file for a simple web application. The application should use the `nginx` image and be accessible on port `8080` on your local machine. Ensure you define the service and specify the port mapping in the compose file.

### Task 2: Add a Custom Network
Modify your `docker-compose.yml` from Task 1 to include a custom network. Define the network at the bottom of your file and assign your service to this network. Research Docker Compose network options to understand how to configure this.

### Task 3: Integrate a Database
Extend your Docker Compose setup by adding a MySQL database service. Ensure the web application and database are on the same network. Use environment variables to set the root password and a database name. Hint: Look into the `environment` key in Docker Compose.

### Task 4: Use Volumes for Persistent Data
For the MySQL service created in Task 3, configure a volume to ensure data persistence. Define the volume at the bottom of your `docker-compose.yml` file and mount it to the appropriate path inside the container. Investigate the correct path for MySQL data storage.