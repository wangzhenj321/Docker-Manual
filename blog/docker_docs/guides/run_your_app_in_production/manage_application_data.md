# Storage overview

By default all files created inside a container are stored on a writable container layer.

Docker has two options for containers to store files in the host machine, so that the files are persisted even after the container stops: **volumes**, and **bind mounts**. If you’re running Docker on Linux you can also use a **tmpfs mount**. If you’re running Docker on Windows you can also use a **named pipe**.

## Choose the right type of mount

No matter which type of mount you choose to use, the data looks the same from within the container. It is exposed as either a directory or an individual file in the container’s filesystem.

<img src="../../../../img/docker_docs/guides/run_your_app_in_production/manage_application_data/type-of-mounts.png">



# Volumes

# Bind mounts

# tmpfs mounts
