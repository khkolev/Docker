# Docker Networks

Docker provides a networking feature that allows containers to communicate with each other and with the outside world. It isolates containers' networking stack to ensure that they can communicate securely. Docker supports multiple network drivers, each designed for specific use cases.

## Understanding Docker Networks
### Default Network Drivers

- **Bridge**: The default network driver for containers, which creates a private internal network on the host.
- **Host**: Removes network isolation between the container and the Docker host, and uses the host’s networking directly.
- **Overlay**: Enables network communication between containers across different Docker hosts.
- **None**: Disables all networking for the container.

## Basic Networking Commands

### Listing Networks

To list all networks on your Docker host:

```bash
docker network ls
```

### Inspecting a Network

To get detailed information about a specific network:

```bash
docker network inspect [NETWORK NAME]
```

### Creating a Network

To create a new network:

```bash
docker network create [NETWORK NAME]
```

### Removing a Network

To remove an existing network:

```bash
docker network rm [NETWORK NAME]
```

## Connecting Containers to Networks

### Connecting a Container to a Network

To connect a running container to a network:

```bash
docker network connect [NETWORK NAME] [CONTAINER ID/NAME]
```

### Disconnecting a Container from a Network

To disconnect a container from a network:

```bash
docker network disconnect [NETWORK NAME] [CONTAINER ID/NAME]
```

## Practical Example: Setting Up a Custom Bridge Network

1. **Create a Custom Bridge Network**:

    ```bash
    docker network create --driver bridge custom-bridge
    ```

2. **Run Containers on the Custom Network**:

    Start two containers and attach them to `custom-bridge`:

    ```bash
    docker run -dit --name container1 --network custom-bridge alpine ash
    docker run -dit --name container2 --network custom-bridge alpine ash
    ```

3. **Test Network Communication**:

    Exec into one container and ping the other by name:

    ```bash
    docker exec -it container1 ping container2
    ```


## Example 2: Custom Subnet and Gateway Configuration

Creating a Docker network with a custom subnet and gateway allows you to integrate Docker containers into your existing network infrastructure seamlessly or to design a network that fits your application's architecture.

### Step 1: Create a Network with a Custom Subnet and Gateway

```bash
docker network create --driver bridge --subnet=192.168.55.0/24 --gateway=192.168.55.1 my-custom-network
```

This command creates a new bridge network named `my-custom-network` with a subnet of `192.168.55.0/24` and a gateway of `192.168.55.1`.

### Step 2: Run Containers on the Custom Network

Run a couple of containers attached to your newly created network:

```bash
docker run -dit --name container1 --network my-custom-network alpine ash
docker run -dit --name container2 --network my-custom-network alpine ash
```

### Step 3: Test Network Connectivity

Verify that the containers can communicate with each other and the gateway:

```bash
docker exec container1 ping -c 4 container2
docker exec container1 ping -c 4 192.168.55.1
```

These commands test the connectivity between `container1` and `container2`, and between `container1` and the network gateway.

## Example 3: Creating an Internal Network

An internal network is used when you want to enable communication between containers without exposing them to the outside world. This is particularly useful for backend services that should not be directly accessible from the host or the internet.

### Step 1: Create an Internal Network

```bash
docker network create --driver bridge --internal my-internal-network
```

This command creates a new bridge network named `my-internal-network` that is internal, meaning containers on this network cannot access the external internet, nor can the external internet access them.

### Step 2: Run Containers on the Internal Network

Start some containers on the internal network:

```bash
docker run -dit --name internal-container1 --network my-internal-network alpine ash
docker run -dit --name internal-container2 --network my-internal-network alpine ash
```

### Step 3: Test Internal Network Communication

Check if the containers can communicate with each other:

```bash
docker exec internal-container1 ping -c 4 internal-container2
```

This command verifies that `internal-container1` can successfully communicate with `internal-container2`.


## Example 4: Creating a Network-Isolated Container with None Driver

For scenarios requiring a container to be completely network-isolated, not just from the external internet but also from other containers, Docker provides the `none` network driver. This setup is ideal for security-critical applications that must not communicate over the network.

### Step 1: Run a Container with Network Isolation

To create a container with no network interfaces (other than the loopback), use the `none` network driver:

```bash
docker run -dit --network none --name network-isolated-container alpine ash
```

This command starts a container named `network-isolated-container` that has no network access, except for the loopback interface, which can only communicate with itself.

### Step 2: Verify Network Isolation

To verify that the container is completely isolated from the network, attempt to ping an external address or even an address on the host machine:

```bash
docker exec network-isolated-container ping -c 4 8.8.8.8
```

This command should fail, indicating that the container cannot access any network outside of its own loopback interface.



## Best Practices in Docker Networks

When working with Docker networks, following best practices can help you maintain a secure, efficient, and scalable container ecosystem:

1. **Use Custom Networks**: Default networks work for simple applications, but custom networks provide better isolation and networking features. Always prefer creating custom networks tailored to your application's needs.

2. **Isolate Sensitive Components**: Use internal networks to isolate sensitive components of your application, such as databases or backend services. This reduces the risk of unauthorized access.

3. **Consistent Subnetting**: Plan your network subnets consistently across your Docker environment. Consistent subnetting avoids IP conflicts and makes network management easier.

4. **Use Network Aliases**: When connecting containers to multiple networks, use network aliases to provide consistent access to services regardless of the network a container is connected to.

5. **Prune Networks Regularly**: Remove unused networks with `docker network prune` to clean up your Docker host and free up resources. Regular pruning helps maintain a clean networking environment.

6. **Secure Overlay Networks**: For applications spanning multiple Docker hosts, use overlay networks with encryption enabled to secure inter-container traffic across hosts.

7. **Monitor Network Performance**: Regularly monitor your Docker networks' performance and use network management tools to identify and resolve bottlenecks or security vulnerabilities.

