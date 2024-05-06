# Docker Networking Homework Assignments

These homework assignments are designed to challenge students on what they have learned from previous guides and practices on Docker networking. Each task will require the application of various Docker networking concepts and commands.

## Task 1: Create a Custom Bridge Network

Create a custom bridge network named `homework-bridge`. Then, run two containers within this network. The first container should be an `nginx` server named `nginx-server`, and the second should be an `alpine` container named `alpine-client`. Verify that `alpine-client` can successfully make an HTTP request to `nginx-server` using `wget` or `curl`.

## Task 2: Inspect Network Configuration

Inspect the `homework-bridge` network you created in Task 1. Extract and list the following information:
- The IP address of `nginx-server`.
- The IP address of `alpine-client`.
- The subnet configuration of `homework-bridge`.

## Task 3: Expose a Container Service to the Host

Run a container on any network of your choice and expose a service (e.g., a web server running on port 80) to the host machine on port 8080. Test accessing this service from the host machine using a web browser or the curl command.

## Task 4: Isolate a Container Completely

Run a container using the `none` network driver. Verify that this container has no access to the internet or any local network. Attempt to ping an external address (e.g., `google.com`) and an address on your local network to demonstrate the isolation.

## Task 5: Clean Up Docker Networks

List all the networks on your Docker host. Identify any networks that are not actively used by containers. Write a bash script to remove all unused networks except the default `bridge`, `host`, and `none` networks. This script should safely check each network for attached containers before attempting to remove it.

---

These tasks are designed to reinforce your understanding of Docker networking concepts, including network creation, inspection, cross-host communication, network isolation, and cleanup. Completing these assignments will help solidify your Docker networking skills.