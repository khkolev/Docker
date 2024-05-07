
**Dockerizing Your Rise App Practice Guide**  This guide will help you dockerize your Rise app, including creating a database backup, setting up a Docker environment, and restoring the database.

1. **Create a Database Backup:**

Follow the steps in "How To Create a Full Backup Using SSMS" to create a backup of your database.

[How to Backup and Restore Database in SQL Server](https://www.infosecurity-magazine.com/blogs/how-to-backup-and-restore-database/)


2. **Dockerize Your App:**

In your video studio, add Orchestration Support to generate a Dockerfile and docker-compose file for your app.

Modify the docker-compose file as follows:

```yaml
version: '3.4'

services:
  airlinesweb:
    # Add your app's code here
    ports: 
      8080:8080
    depends_on:
      - mssql

  mssql:
    image: "mcr.microsoft.com/mssql/server"
    container_name: mssql
    environment:
      SA_PASSWORD: "Password10!n"
      ACCEPT_EULA: "Y"
    volumes:
      - mssql-data:/var/opt/mssql
    ports:
      # The default port of SQL Server is 1433.
      # Map the container's port 1433 to your local port 1433.
      1433:1433

volumes:
  mssql-data:
    # Use the local driver by default.
    driver: local
```

3. **Update the Connection String:**

In your app's connection string, replace the hostname "localhost,1433" with "mssql,1433".

Example:

```
"Local": "Server=mssql,1433;Initial Catalog=Rise;User ID=SA;Password='Password10!n';TrustServerCertificate=True;"
```

4. **Copy the Database Backup to the Container:**

Use the following Docker command to copy the backup file to the container:

```bash
docker cp Rise.bak mssql:/var/backups
```

5. **Restore the Database:**

To restore the database using SSMS, follow the steps in "How to Restore a Differential Backup Using SSMS".

[How to Backup and Restore Database in SQL Server](https://www.infosecurity-magazine.com/blogs/how-to-backup-and-restore-database/)


GLHF