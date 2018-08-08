# drone-docker

[![Build Status](http://beta.drone.io/api/badges/drone-plugins/drone-docker/status.svg)](http://beta.drone.io/drone-plugins/drone-docker)
[![Go Doc](https://godoc.org/github.com/drone-plugins/drone-docker?status.svg)](http://godoc.org/github.com/drone-plugins/drone-docker)
[![Go Report](https://goreportcard.com/badge/github.com/drone-plugins/drone-docker)](https://goreportcard.com/report/github.com/drone-plugins/drone-docker)
[![Join the chat at https://gitter.im/drone/drone](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/drone/drone)

Drone plugin can be used to build and publish Docker images to a container
registry. For the usage information and a listing of the available options
please take a look at [the docs](http://plugins.drone.io/drone-plugins/drone-docker/).

Note: This is a fork of the original plugin by Drone. It adds the prune flag that allows you
to disable the prune functionality. Example usage:

```
pipeline:
  build:
    image: chatkitinc/drone-docker
    repo: <your repo>
    registry: <your registry>
    username: ${REGISTRY_USERNAME}
    password: ${REGISTRY_PASSWORD}
    prune: false
```

## Build

Build the binary with the following commands:

```
go build
go test
```

## Docker

Build the docker image with the following commands:

```
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -tags netgo
docker build --rm=true -t chatkitinc/drone-docker .
```

Please note incorrectly building the image for the correct x64 linux and with
GCO disabled will result in an error when running the Docker image:

```
docker: Error response from daemon: Container command
'/bin/drone-docker' not found or does not exist..
```

## Usage

Execute from the working directory:

```
docker run --rm \
  -e PLUGIN_TAG=latest \
  -e PLUGIN_REPO=octocat/hello-world \
  -e DRONE_COMMIT_SHA=d8dbe4d94f15fe89232e0402c6e8a0ddf21af3ab \
  -v $(pwd):$(pwd) \
  -w $(pwd) \
  --privileged \
  chatkitinc/drone-docker --dry-run
```
