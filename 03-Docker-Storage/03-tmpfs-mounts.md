# Docker Storage: tmpfs Mounts
## Introduction to tmpfs Mounts in Docker
In Docker, besides volumes and bind mounts, there's a third option for managing data - tmpfs mounts. This feature is particularly useful for temporary storage of sensitive files that you don't want to persist on the host or within the container's writable layer. It's important to note that tmpfs mounts are only available on Linux systems.

## Understanding tmpfs Mounts

Tmpfs mounts allow containers to create files outside their writable layer, directly in the host's memory. This means that when the container stops, the tmpfs mount and its files are removed, ensuring no persistence of the temporary data.

### Limitations

- Tmpfs mounts cannot be shared between containers.
- Available only on Linux.
- Permissions on tmpfs may reset after a container restart, though setting the uid/gid can be a workaround.

### Choosing Between `--tmpfs` and `--mount` Flags

- `--tmpfs`: Mounts a tmpfs without configurable options, suitable for standalone containers.
- `--mount`: More verbose, allowing for configurable options like `tmpfs-size` and `tmpfs-mode`.

## Examples

### Using `--mount` for tmpfs

```bash
docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app \
  nginx:latest
```

### Verifying the tmpfs Mount

To verify the mount:

```bash
docker inspect tmptest --format '{{ json .Mounts }}'
```

You should see output similar to:

```json
[{"Type":"tmpfs","Source":"","Destination":"/app","Mode":"","RW":true,"Propagation":""}]
```

### Stopping and Removing the Container

```bash
docker stop tmptest
docker rm tmptest
```

### Using `--tmpfs` Flag

For a simpler approach without configurable options:

```bash
docker run -d \
  -it \
  --name tmptest \
  --tmpfs /app \
  nginx:latest
```

### Specifying tmpfs Options

To specify options like size and mode, use the `--mount` flag:

```bash
docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app,tmpfs-mode=1770 \
  nginx:latest
```

## Best Practices

Tmpfs mounts offer a secure and temporary way to handle sensitive data within Docker containers. Remember, this feature is specific to Linux and comes with its own set of limitations and considerations.