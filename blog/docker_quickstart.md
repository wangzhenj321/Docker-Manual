# Part 1: Orientation and setup

## Docker concepts

Docker is a platform for developers and sysadmins to build, run, and share applications with containers. The use of containers to deploy applications is called containerization. Containers are not new, but their use for easily deploying applications is.

### Images and containers

Fundamentally, a container is nothing but a running process, with some added encapsulation features applied to it in order to keep it isolated from the host and from other containers. One of the most important aspects of container isolation is that each container interacts with its own private filesystem; this filesystem is provided by a Docker image. An image includes everything needed to run an application - the code or binary, runtimes, dependencies, and any other filesystem objects required.

### Containers and virtual machines

A container runs natively on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.

By contrast, a virtual machine (VM) runs a full-blown "guest" operating system with virtual access to host resources through a hypervisor. In general, VMs incur a lot of overhead beyond what is being consumed by your application logic.

<>

## References

1. [Orientation and setup](https://docs.docker.com/get-started/)

# Part 2: Build and run your image

## Set up

Let us download an example project from the Docker Samples page.

```
git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board/bulletin-board-app
```

The `node-bulletin-board` project is a simple bulletin board application, written in Node.js. In this example, let’s imagine you wrote this app, and are now trying to containerize it.

## Define a container with Dockerfile

Take a look at the file called `Dockerfile` in the bulletin board application. Dockerfiles describe how to assemble a private filesystem for a container, and can also contain some metadata describing how to run a container based on this image. The bulletin board app Dockerfile looks like this:

```
# Use the official image as a parent image.
FROM node:current-slim

# Set the working directory.
WORKDIR /usr/src/app

# Copy the file from your host to your current location.
COPY package.json .

# Run the command inside your image filesystem.
RUN npm install

# Inform Docker that the container is listening on the specified port at runtime.
EXPOSE 8080

# Run the specified command within the container.
CMD [ "npm", "start" ]

# Copy the rest of your app's source code from your host to your image filesystem.
COPY . .
```

Writing a Dockerfile is the first step to containerizing an application. You can think of these Dockerfile commands as a step-by-step recipe on how to build up your image. This one takes the following steps:

- Start `FROM` the pre-existing `node:current-slim` image. This is an official image, built by the node.js vendors and validated by Docker to be a high-quality image containing the Node.js Long Term Support (LTS) interpreter and basic dependencies.
- Use `WORKDIR` to specify that all subsequent actions should be taken from the directory `/usr/src/app` in your image filesystem (never the host’s filesystem).
- `COPY` the file `package.json` from your host to the present location (`.`) in your image (so in this case, to `/usr/src/app/package.json`)
- `RUN` the command `npm install` inside your image filesystem (which will read `package.json` to determine your app’s node dependencies, and install them)
- `COPY` in the rest of your app’s source code from your host to your image filesystem.

You can see that these are much the same steps you might have taken to set up and install your app on your host. However, capturing these as a Dockerfile allows you to do the same thing inside a portable, isolated Docker image.

The steps above built up the filesystem of our image, but there are other lines in your Dockerfile.

The `CMD` directive is the first example of specifying some metadata in your image that describes how to run a container based on this image. In this case, it’s saying that the containerized process that this image is meant to support is `npm start`.

The `EXPOSE 8080` informs Docker that the container is listening on port 8080 at runtime.

What you see above is a good way to organize a simple Dockerfile; always start with a `FROM` command, follow it with the steps to build up your private filesystem, and conclude with any metadata specifications. 

## Build and test your image

Make sure you’re in the directory `node-bulletin-board/bulletin-board-app` in a terminal or PowerShell using the `cd` command. Let’s build your bulletin board image:

```
docker build --tag bulletinboard:1.0 .
```

You’ll see Docker step through each instruction in your Dockerfile, building up your image as it goes. If successful, the build process should end with a message `Successfully tagged bulletinboard:1.0`.

## Run your image as a container

1. Start a container based on your new image:

    ```
    docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
    ```

2. Visit your application in a browser at `ocalhost:8000` You should see your bulletin board application up and running.

3. Once you’re satisfied that your bulletin board container works correctly, you can delete it:

    ```
    docker rm --force bb
    ```

## References

1. [Build and run your image](https://docs.docker.com/get-started/part2/)

# Part 3: Share images on Docker Hub

## Create a Docker Hub repository and push your image

Now let’s make our first repo, and share our bulletin board app there.

> You can do the 'Sign in' from the command line by typing `docker login`.

1. Click on the Docker icon in your menu bar, and navigate to Repositories -> Create. You’ll be taken to a Docker Hub page to create a new repository.

2. Fill out the repository name as bulletinboard. Leave all the other options alone for now, and click Create at the bottom.

3. Now you are ready to share your image on Docker Hub, but there’s one thing you must do first: images must be namespaced correctly to share on Docker Hub. Specifically, you must name images like `<Docker ID>/<Repository Name>:<tag>`. You can relabel your `bulletinboard:1.0` image like this:

    ```
    docker tag bulletinboard:1.0 gordon/bulletinboard:1.0
    ```

4. Finally, push your image to Docker Hub:

    ```
    docker push gordon/bulletinboard:1.0
    ```
    
    Visit your repository in Docker Hub, and you’ll see your new image there. Remember, Docker Hub repositories are public by default.


