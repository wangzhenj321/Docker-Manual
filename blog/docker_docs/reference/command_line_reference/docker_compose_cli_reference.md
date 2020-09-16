| Commands | Description |
| --- | --- |
| `down` | Stops containers and removes containers, networks, volumes, and images created by `up`. |
| `exec` | This is the equivalent of `docker exec`. With this subcommand you can run arbitrary commands in your services. Commands are by default allocating a TTY, so you can use a command such as `docker-compose exec web sh` to get an interactive prompt. |
| `pause` | Pauses running containers of a service. They can be unpaused with `docker-compose unpause`. |
| `unpause` | Unpauses paused containers of a service. |
| `ps` | Lists containers. |
| `stop` | Stops running containers without removing them. They can be started again with `docker-compose start`. |
| `start` | Starts existing containers for a service. |
| `up` | Builds, (re)creates, starts, and attaches to containers for a service.<br><br>If there are existing containers for a service, and the service’s configuration or image was changed after the container’s creation, `docker-compose up` picks up the changes by stopping and recreating the containers (preserving mounted volumes). To prevent Compose from picking up changes, use the `--no-recreate` flag. |
