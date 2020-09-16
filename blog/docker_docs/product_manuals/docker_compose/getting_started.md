**Table of contents**

- [Step 1: Setup](#step-1-setup)
- [Step 2: Create a Dockerfile](#step-2-create-a-dockerfile)
- [Step 3: Define services in a Compose file](#step-3-define-services-in-a-compose-file)
- [Step 4: Build and run your app with Compose](#step-4-build-and-run-your-app-with-compose)
- [Step 5: Edit the Compose file to add a bind mount](#step-5-edit-the-compose-file-to-add-a-bind-mount)
- [Step 6: Re-build and run the app with Compose](#step-6-re-build-and-run-the-app-with-compose)
- [Step 7: Update the application](#step-7-update-the-application)

## Step 1: Setup

1. Create a directory for the project:

    ```
    $ mkdir composetest
    $ cd composetest
    ```

2. Create a file called `app.py` in your project directory and paste this in:

    ```python
    import time

    import redis
    from flask import Flask

    app = Flask(__name__)
    cache = redis.Redis(host='redis', port=6379)


    def get_hit_count():
        retries = 5
        while True:
            try:
                return cache.incr('hits')
            except redis.exceptions.ConnectionError as exc:
                if retries == 0:
                    raise exc
                retries -= 1
                time.sleep(0.5)


    @app.route('/')
    def hello():
        count = get_hit_count()
        return 'Hello World! I have been seen {} times.\n'.format(count)
    ```

3. Create another file called `requirements.txt` in your project directory and paste this in:

    ```
    flask
    redis
    ```

## Step 2: Create a Dockerfile

In your project directory, create a file named `Dockerfile` and paste the following:

```
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

## Step 3: Define services in a Compose file

Create a file called `docker-compose.yml` in your project directory and paste the following:

```
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

## Step 4: Build and run your app with Compose

1. From your project directory, start up your application by running `docker-compose up`.

2. Enter `http://localhost:5000/` in a browser to see the application running.

3. Refresh the page.

4. Switch to another terminal window, and type `docker image ls` to list local images.

5. Stop the application, either by running `docker-compose down` from within your project directory in the second terminal, or by hitting CTRL+C in the original terminal where you started the app.

## Step 5: Edit the Compose file to add a bind mount

Edit `docker-compose.yml` in your project directory to add a bind mount for the `web` service:

```
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
    environment:
      FLASK_ENV: development
  redis:
    image: "redis:alpine"
```

## Step 6: Re-build and run the app with Compose

From your project directory, type `docker-compose up` to build the app with the updated Compose file, and run it.

## Step 7: Update the application

Because the application code is now mounted into the container using a volume, you can make changes to its code and see the changes instantly, without having to rebuild the image.
