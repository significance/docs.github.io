---
title: Bee Using Docker
id: docker
---

Bee is also provided as Docker images hosted at [Docker Hub](https://hub.docker.com/r/ethersphere/bee).

### Quick Start

Try Bee out by simply running the following command in your Terminal. 

```sh
docker run --rm -it ethersphere/bee\
  start --welcome-message="Hi I am a very buzzy bee bzzzz bzzz bzz. 🐝"
```

To persist files mount a local directory as follows and enter the password used to encrypt your keyfiles.

```sh
docker run\
  -v /path/to/.bee-docker:/home/bee/.bee\
  --rm -it ethersphere/bee\
  start
```

Once you have generated your keys, leave Bee to run in the background...

```sh
docker run\
  -v /path/to/.bee-docker:/home/bee/.bee\
  -d ethersphere/bee\
  start\
  --welcome-message="Bzzzz bzzz bzz bzz. 🐝"
```

Note, Docker insists on absolute paths so you must replace /path/to/.bee-docker with a valid path from your local filesystem.

### Other Versions

You other versions of the Bee container are also available.

#### Specific Versions

```sh
docker pull ethersphere/bee:0.2.0
```

#### Edge

```sh
docker pull ethersphere/bee:latest
```

Please see the [Docker Hub repository](https://hub.docker.com/r/ethersphere/bee) for more information.