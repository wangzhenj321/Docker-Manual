# Dockerfile reference

## Instructions

| Instructions | Explanation |
| --- | --- |
| `FROM` | The `FROM` instruction initializes a new build stage and sets the **Base Image** for subsequent instructions. |
| `RUN` | The `RUN` instruction will execute any commands in a new layer on top of the current image and commit the results. |
| `CMD` | The main purpose of a `CMD` is to provide defaults for an executing container. |
| `LABEL` | The `LABEL` instruction adds metadata to an image. |
| `EXPOSE` | The `EXPOSE` instruction informs Docker that the container listens on the specified network ports at runtime. |
| `ENV` | The `ENV` instruction sets the environment variable `<key>` to the value `<value>`. |
| `ADD` | The `ADD` instruction copies new files, directories or remote file URLs from `<src>` and adds them to the filesystem of the image at the path `<dest>`. |
| `COPY` | The `COPY` instruction copies new files or directories from `<src>` and adds them to the filesystem of the container at the path `<dest>`. |
| `ENTRYPOINT` | An `ENTRYPOINT` allows you to configure a container that will run as an executable. |
| `VOLUME` | The `VOLUME` instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers. |
| `USER` | The `USER` instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any `RUN`, `CMD` and `ENTRYPOINT` instructions that follow it in the `Dockerfile`. |
| `WORKDIR` | The `WORKDIR` instruction sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` and `ADD` instructions that follow it in the `Dockerfile`. |
| `ARG` | The `ARG` instruction defines a variable that users can pass at build-time to the builder with the `docker build` command using the `--build-arg <varname>=<value>` flag. |
| `ONBUILD` | The `ONBUILD` instruction adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build. |
| `STOPSIGNAL` | The `STOPSIGNAL` instruction sets the system call signal that will be sent to the container to exit. |
| `HEALTHCHECK` | The `HEALTHCHECK` instruction tells Docker how to test a container to check that it is still working. |
| `SHELL` | The `SHELL` instruction allows the default shell used for the shell form of commands to be overridden. |

## References

1. [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
