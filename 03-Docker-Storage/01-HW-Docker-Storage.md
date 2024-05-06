# Homework Docker Volumes 
## Task 1: Volume Sharing Between Containers

Create two containers that share a volume. Use this shared volume to exchange data between the containers.

1. Create a volume named `shared-data`.
2. Run a container named `producer` that mounts `shared-data` and writes a message to a file within the volume.
3. Run another container named `consumer` that mounts the same `shared-data` volume and reads the message from the file.

## Task 2: Database Backup and Restore

Practice backing up and restoring data from a Dockerized database using volumes.

1. Run a MySQL container with a named volume `db-data` for its data storage.
2. Populate the database with sample data.
3. Backup the `db-data` volume to a tar file.
4. Restore the database in a new container using the backup file.

## Task 3: Volume Migration

Migrate a volume from one Docker host to another. This task simulates moving data in a production environment.

1. On the original Docker host, create a volume `migrate-me` and populate it with data.
2. Backup the volume to a file.
3. Transfer the backup file to a new Docker host.
4. Restore the volume on the new host and verify the data integrity.

## Task 4: Implementing Read-Only Volumes

Explore the read-only option for Docker volumes to understand its impact on containerized applications.

1. Create a volume `readonly-data` and add some data to it.
2. Run a container that mounts `readonly-data` in read-only mode.
3. Inside the container, attempt to modify the data in the volume to observe the behavior.

## Task 5: Volume Cleanup Strategy

Develop a strategy for identifying and removing unused Docker volumes to free up space on your system.

1. List all volumes on your Docker host and identify any unused volumes.
2. Write a script or command sequence to safely remove unused volumes, ensuring no data loss for active containers.
3. Test your cleanup strategy by creating and removing several volumes, verifying that only the correct volumes are removed.

