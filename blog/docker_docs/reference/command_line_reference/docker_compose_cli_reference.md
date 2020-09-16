## `docker-compose up`

```
Usage: up [options] [--scale SERVICE=NUM...] [SERVICE...]
```

If there are existing containers for a service, and the service’s configuration or image was changed after the container’s creation, `docker-compose up` picks up the changes by stopping and recreating the containers (preserving mounted volumes). To prevent Compose from picking up changes, use the `--no-recreate` flag.
