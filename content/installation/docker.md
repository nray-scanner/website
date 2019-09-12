---
title: "Docker"
weight: 230
---

Starting with 1.1, there are official Docker images and care is taken to support running nray from containered environments.

#### Running nray from Docker

Nray's source repository contains two Dockerfiles that are used to build the images also found on Docker Hub. 
The first one is based on Docker's scratch image and since there is no user space apart from nray, it is really small.
The second one builds upon Debian, giving the user the ability to access the system interactively which is often more desirable than having a small container.

##### Example: Server

In order to run a nray server from a container, a few precautions have to be taken:

- Make sure to bind to 0.0.0.0 inside the container (`host: "0.0.0.0"`), otherwise it is not possible to connect to the nray instance.
- Make sure to read configuration and write results to a directory that exists within the container and is mounted to the outside world. 
The images contain the directory `/nray-data/` which is readable and writable for the nray user. 
In this example, `/tmp/nray` is mounted into the container - now, the nray process inside the container is able to read the configuration and if the output is configured to be written to `/nray-data/`, it can be read by the host.

A command that spawns a container running a nray server with respective directories mounted and ports forwarded may look like this:

~~~bash
docker run --rm --mount type=bind,src=/tmp/nray,dst=/nray-data -p 8601:8601 nrayscanner/nray-scratch server -c /nray-data/nray-conf.yaml
~~~

##### Example: Node

Compared to the server, nodes are a simple case since they are able to run without binding to ports or accessing the disk.
Therefore, running a node can be as simple as:

~~~bash
docker run --rm nrayscanner/nray-debian node -s <server URL> -p <server port>
~~~

#### Building nray docker containers

Please refer to the Dockerfiles in the `docker/` directory that can be found in the source repository.
The creation of the images is done via the `docker` target in the Makefile. 

#### Building nray binaries from a docker container

In order to build nray within a docker container, e.g. to avoid setting up a Go build environment on your own or because you are in a hurry and it is a one-liner, run the following command in the root of the nray source code repository:

~~~bash
docker run --rm -v "$PWD":/nray -w /nray golang:latest make release
~~~

If you are only interested in binaries for a specific architecture, you may alter the make target from `release` to any other supported value, e.g. `build-x64-windows`.