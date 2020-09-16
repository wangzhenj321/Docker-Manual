- `docker-compose down [options]`

    Stops containers and removes containers, networks, volumes, and images created by `up`.

- `docker-compose exec [options] [-e KEY=VAL...] SERVICE COMMAND [ARGS...]`

    This is the equivalent of `docker exec`. With this subcommand you can run arbitrary commands in your services. Commands are by default allocating a TTY, so you can use a command such as `docker-compose exec web sh` to get an interactive prompt.

- `docker-compose ps [options] [SERVICE...]`

    Lists containers.

- `docker-compose up [options] [--scale SERVICE=NUM...] [SERVICE...]`

    Builds, (re)creates, starts, and attaches to containers for a service.

    If there are existing containers for a service, and the service’s configuration or image was changed after the container’s creation, `docker-compose up` picks up the changes by stopping and recreating the containers (preserving mounted volumes). To prevent Compose from picking up changes, use the `--no-recreate` flag.
