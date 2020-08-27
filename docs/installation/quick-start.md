---
title: Quick Start
id: quick-start
---

## Supported platforms

The client can be installed on MacOS, Windows and various Linux flavors.

### Quick Install

We provide a convenient [install script](https://github.com/ethersphere/bee/blob/637b67a8e0a2b15e707f510bb7f49aea4ef6c110/install.sh), which automatically detects your execution environment and installs the latest stable version of the Bee client on your computer.

Simply run one of the following commands in your Terminal...

- Using wget:
```console
wget -q -O - https://raw.githubusercontent.com/ethersphere/bee/master/install.sh | TAG=v0.2.0 bash
```a
- Using curl:
```console
curl -s https://raw.githubusercontent.com/ethersphere/bee/master/install.sh | TAG=v0.2.0 bash
```

#### Edge

:::info
Find the latest release of Bee by navigating to [bee](https://github.com/ethersphere/bee/releases/tag/) and use this release (e.g. v0.2.0) behind the TAG= in the commands above
:::

- Using wget:
 ```console
 wget -q -O - https://raw.githubusercontent.com/ethersphere/bee/master/install.sh | bash
 ```

 - Using curl:
 ```console
 curl -s https://raw.githubusercontent.com/ethersphere/bee/master/install.sh | bash
 ```

:::caution
If you choose to use the latest master branch at github, this documentation is not guaranteed to be up-to-date and some features may be unstable.
:::