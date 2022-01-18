![alt Narwhal logo](logo.png)

# Narwhal: FastAPI + Docker + Poetry-based Python server

Narwhal provides a simple server template you can use to quickly build a [FastAPI](https://fastapi.tiangolo.com/)-based server application written in [Python](https://www.python.org/) that can be easily deployed as an ultra-lightweight Docker container, making it ideal for deploying your app on [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/), [AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html), [Google Cloud Run](https://cloud.google.com/run) and others.

# Main Features

- Uses [FastAPI](https://fastapi.tiangolo.com/uk/deployment/server-workers/) as server framework. 🚀️

- Pre-configured to use [uvicorn](https://www.uvicorn.org/) and [uvloop](https://github.com/MagicStack/uvloop) for lightning-fast performance. ⚡️

- Uses [Poetry](https://python-poetry.org/docs/) for easily managing dependencies. ✨️

- Speeds up development via hot reloading. 🪄️

- Super lightweight container images thanks to [multi-stage](https://docs.docker.com/develop/develop-images/multistage-build/) Docker build and [Alpine Linux](https://www.alpinelinux.org/about/) (starts at ~70MiB). 🪶️

- Docker image pre-configured to run as a non-root user by default for extra safety. 🔒️

# Dependencies

Make sure you have the following dependencies installed to run in development mode:

- Poetry
- Docker
- Make (for running various pre-configured commands)

# Getting started

## Clone the project

```bash
$ git clone git@github.com:ApsisTechnologies/FastAPI-Docker-Template.git
```
## Run in development mode

```bash
$ cd FastAPI-Docker-Template

# start local server on localhost, port 8000
$ make dev
```
## Run as a Docker container

```bash
# run container, also on localhost, port 8000
$ make serve
```

# Notes

### Application source code

The `src` directory contains the application code which is deployed onto the container image.

You'll need to modify `Dockerfile` if you wanted to include other source code locations in your app.

### Docker image naming

The name of the Docker image is derived from the `name` and `version` fields inside `pyproject.toml`. The `Makefile` configuration extracts these fields automatically and passes them to Docker to tag the image as `"<project name>:<project version>"`.

### CORS support

The application is pre-configured to support [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) headers.

### Header proxying

The Docker image passes `--proxy-headers` as a `uvicorn` parameter so that your app can run behind a server that takes care of HTTPS. If this is not the case for your app you'll need to modify `Dockerfile` to remove this flag.

### Non-root image user

Most Linux images run as root by default which is a dangerous practice. The image comes pre-configured to run as a non-root user, only using `root` user access during the build stages.

See `Dockerfile` for more details.

### Modifying Python version

This project uses Python v3.9 by default. To modify this you can modify the line `ARG PYTHON_VERSION=3.9` inside `Dockerfile`.
