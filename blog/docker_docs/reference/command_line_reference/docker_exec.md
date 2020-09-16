## Description

Run a command in a running container

## Usage

```
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

## Extended description

The `docker exec` command runs a new command in a running container.

The command started using `docker exec` only runs while the container’s primary process (`PID 1`) is running, and it is not restarted if the container is restarted.

COMMAND will run in the default directory of the container. If the underlying image has a custom directory specified with the WORKDIR directive in its Dockerfile, this will be used instead.

COMMAND should be an executable, a chained or a quoted command will not work. 

## Options

- `--interactive , -i`

    Keep STDIN open even if not attached

- `--tty , -t`

    Allocate a pseudo-TTY
