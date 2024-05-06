# Configure Your Environment 

## Variant A: Docker Desktop on Windows
[Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)

## Variant B: VirtualBox with Linux & Docker
### [Watch this video tutorial](https://www.youtube.com/watch?v=UZYOAec2HFo) to see all the steps in action.

### 1. Download everything you need. 

[Oracle VM VirtualBox](https://www.virtualbox.org/ "Oracle VM VirtualBox")
- Donwload Virtual Box and the VirtualBox Extension Pack.

[Debian](https://www.debian.org/download "Getting Debian")
- Download __debian-12.5.0-amd64-netinst.iso.__.

[Download PuTTY](https://www.putty.org/ "Getting Debian")
- Download PuTTY SSH Client.

___
### 2. Install Virtual Box add theVirtualBox Extension Pack.
 
  1. Create New Virtual Machine.
        - Use debian-12.5.0-amd64-netinst.iso.;
        - Check **"Skip Unattended Install**;
        - Partitioning Method: "Guided - use entire disk and set up LVM";
        - Choose only SSH Server & standard system utilities;
        - After Installtion shutdown the machine.

  2. Set up port forwarding between the virtual machine and the host machine for ports:
        - VM 22 port --> Host 22 Port;
        - VM 80 port --> Host 80 Port;
        - VM 100 port --> Host 100 Port;
        - VM 3306 port --> Host 3306 Port;
        - VM 8080 port --> Host 8080 Port;

  3. Create a snapshot of the VM before continuing with the installation of Docker.
___
### 3. Install PuTTY SSH Client
  1. Make SSH connect as use __localhost__ and port 22
___

### 4.  Install Docker
  1. Login as a root
  2. Update the apt package index and install packages to allow apt to use a repository over HTTPS:
  ~~~
  apt-get update
  apt-get install ca-certificates curl gnupg lsb-release
  ~~~
  2. Add Docker’s official GPG key:
  ~~~
  install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
  ~~~
  3. Use the following command to set up the repository:
  ~~~
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
  ~~~
  4. Update the apt package index:
  ~~~
  apt-get update
  ~~~
  5. Install Docker Engine, containerd, and Docker Compose.
  ~~~
  apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ~~~
  6. Add your user to the docker group.
  ~~~
  usermod -aG docker student
  ~~~
  7. Verify that the Docker Engine installation is successful and that port forwarding between the virtual machine and the host is working by running a Docker image that maps to port 80.
  ```mermaid
graph LR
    Container --- VM --- Host
```
  ~~~
  docker run -d -p 80:80 docker/getting-started
  ~~~

[WEB - Docker Getting Started](http://localhost/ "WEB - Docker Getting Started")

With these steps, you will have successfully configured your development environment with the required components.


