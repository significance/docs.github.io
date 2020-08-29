---
title: Build from Source
id: build-from-source
---

Bee is written using the [Go](https://golang.org) language. 

You may build the software directly from the [source](https://github.com/ethersphere/bee).

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

3) Checkout the required release:

```sh
git checkout master
```

4) Build the binary:

```sh
make binary
```

5) Check you are able to run the `bee` command. Success can be verified by running:
```sh
dist/bee version
> 0.2.0
```

6) (optional) Additionally, you may also like to move the Bee binary to somewhere in your `$PATH`
```sh
sudo cp dist/bee /usr/local/bin/bee
```