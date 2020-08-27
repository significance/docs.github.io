---
title: Build from Source
id: build-from-source
---

Bee is written using the Go language. You may build the software directly from the [source](https://github.com/ethersphere/bee).

Prerequisites for installing Bee from source are:

- Go - download the latest release from [golang.org](https://golang.org/dl),
- git - download from [git-scm.com](https://git-scm.com/) or install with your package manager,
- make - usually installed as default

### Build from Source

1) Clone the repository:
```sh
git clone https://github.com/ethersphere/bee
cd bee
```

2) Use `git` to find the latest release:
```sh
git describe --tags
```

3) Checkout the latest release:

```sh
git checkout <name_of_latest_tag>
```

4) Build the binary and move the binary to a directory in your `$PATH`:

```sh
make binary
cp dist/bee /usr/local/bin/bee
```

5) You check you are able to run the `bee` command, which you can verify by running:
```sh
bee version
```

This will now return the version number for the Bee client you are running.