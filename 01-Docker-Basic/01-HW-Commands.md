
### Homework Assignments on Docker Basic

1. **Pull and Inspect an Apache Image**
    -  **Task**: Use Docker to pull the official Apache    (httpd) image from Docker Hub. After pulling the   image, use the docker image inspect command to    inspect the image. In your response, include the   command you used to pull the image and a brief    summary of one section of the output from the  inspect command (e.g., the "Env" section showing     environment variables).

    - **Response Format**: Text response including the    command used and a summary of the inspection   output.

2. **Run an Apache Container and Access It**
    - **Task**: Run a container using the Apache image you pulled in the previous assignment. Map the container's 80 port to a free port on your host machine. After the container is running, access the default Apache page from your browser using the host machine's IP and the mapped port. Provide the command you used to run the container and describe what you see when accessing the Apache page from your browser.

    - **Response Format**: Text response including the command used and a description of the Apache default page.

3. **Customize and Serve Custom HTML with Apache**
    - **Task**: Create a simple HTML file on your host machine named index.html with custom content (e.g., "Hello, Docker!"). Copy this file into your running Apache container to the directory `/usr/local/apache2/htdocs/`, replacing the default index.html. Provide the command you used to copy the file into the container. Then, access the Apache server from your browser again and describe the new content you see.

    - **Response Format**: Text response including the command used to copy the file and a description of the new content on the Apache page.

4. **Inspect and Log Apache Container Activities**
    - **Task**: Use the docker container inspect command to inspect your running Apache container. Focus on finding and summarizing the "State" section, which includes the container's running status, and whether it's paused or restarted. Next, use the docker logs [CONTAINER ID/NAME] command to view the logs of your Apache container. Summarize any interesting findings from the logs, such as HTTP requests.

    - **Response Format**: Text response including a summary of the "State" section from the inspection output and interesting log entries.

5. **Stop, Remove, and Clean Up Containers and Images**
    - **Task**: Stop your running Apache container using the docker stop command. Then, remove this container using the docker container rm command. Finally, clean up any unused Docker images from your system using the docker image prune command. Provide the commands you used for these tasks and describe what each command does.

    - **Response Format**: Text response including the commands used and a brief explanation of what each command does.