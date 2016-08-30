# docker-alpine-python

[![Docker Stars](https://img.shields.io/docker/stars/sruml/alpine-python.svg)][hub]
[![Docker Pulls](https://img.shields.io/docker/pulls/sruml/alpine-python.svg)][hub]
[![Docker Layers](https://badge.imagelayers.io/sruml/alpine-python:latest.svg)](https://imagelayers.io/?images=sruml/alpine-python:latest 'Get your own badge on imagelayers.io')

[hub]: https://hub.docker.com/r/sruml/alpine-python/

Docker containers for running Python applications, based on Alpine Linux with s6 for process management. The goal is to provide small and reliable containers to run Python applications (e.g. Flask web apps).

The containers are based on the _alpine-base_ containers from [smebberson/docker-alpine](https://github.com/smebberson/docker-alpine/tree/master/alpine-base). The _alpine-base_ containers provides highly configurable Docker images running [Alpine Linux](https://www.alpinelinux.org/) and [s6](http://skarnet.org/software/s6/) process management.


## Features

This image features:

  * [Alpine Linux](https://www.alpinelinux.org/)
  * [s6](http://skarnet.org/software/s6) and [s6-overlay](https://github.com/just-containers/s6-overlay)
  * [Python](https://www.python.org/)


## Supported Tags

  * **2.7 ([Dockerfile](https://github.com/hypebeast/docker-alpine-python/blob/master/2.7/Dockerfile))**
  * **2.7-onbuild ([Dockerfile](https://github.com/hypebeast/docker-alpine-python/blob/master/2.7/onbuild/Dockerfile))**
  * **3.5 ([Dockerfile](https://github.com/hypebeast/docker-alpine-python/blob/master/3.5/Dockerfile))**
  * **3.5-onbuild ([Dockerfile](https://github.com/hypebeast/docker-alpine-python/blob/master/3.5/onbuild/Dockerfile))**

**Note**

The `onbuild` images are running `pip install -r requirements.txt` during the build. This ensures that the dependencies are cached during the build. In order to make this work ensure that your `requirements.txt` file are in the same directory.


## Goals

  * Provide small Docker images for Python applications
  * The containers should be highly and simple configurable
  * Usage of s6-supervise as a simple and reliable process manager


## Usage

The command `python` is started during the start of a container. But you can also specify your own command:

```shell
docker run -rm -it -v "$(pwd)":/app -w /app sruml/alpine-python:2.7 python app.py
```

### Using a custom Dockerfile

In most cases you will extend this Docker image in order to run your own  application.

The following example shows how to run a simple web application (e.g. Flask app):

```dockerfile
FROM sruml/alpine-python:2.7-onbuild

# Expose the port for the Flask app
EXPOSE 5000

# Run the Flask app
CMD python flask_app.py
```

Build your image:

```shell
docker build -i hypebeast/webapp .
```

Mount your application folder into the container and run it:

```shell
docker run -rm -v "$(pwd)":/app -w /app -p 5000:5000 hypebeast/webapp
```

### Use the s6-supervise process manager

A better way to run a Python application as aservice is to use the _s6-supervise_ process manager.

In order to use s6-supervise to manage your application you need to create a _run_ file and put it to the `/etc/services.d` directory.

```dockerfile
TODO
```


## License

The code in this repository, unless otherwise noted, is MIT licensed. See the `LICENSE` file in this repository.


## Credits

  * [alpine-python](https://github.com/jfloff/alpine-python)
  * [docker-alpine](https://github.com/smebberson/docker-alpine)
