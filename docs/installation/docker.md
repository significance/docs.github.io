---
title: Installing Bee with Docker
id: docker
---

Bee is provided as Docker images hosted at [Dockerhub](https://hub.docker.com/r/ethersphere/bee).

### Quick Start

Try Bee by simply running the following command in your Terminal.

```sh
	docker run -it ethersphere/bee:0.2.0 start --help
```

To persist files mount a local directory as follows

```sh
	docker run -v /home/<user>/.bee-docker:/home/bee/.bee -it ethersphere/bee:0.2.0 start
```

### Other Versions

You may also pull the current Bee container by running.

#### Latest Version

```sh
$ docker pull ethersphere/bee:0.2.0
```

#### Edge

`docker pull ethersphere/bee:latest`

Please see [Dockerhub](https://hub.docker.com/r/ethersphere/bee) for more information.