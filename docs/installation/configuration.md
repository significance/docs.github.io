---
title: Configuring Your Bee Node
id: configuration
---

Your Bee node can be configured by adding arguments terminal command on startup. 

Run `bee start --help` in your Terminal to get the list of available command line arguments.

#### Example

In this example, we change the port that the Bee API runs on, enable the Debug API, and set it to listen on port 6666.

```console
bee start \
  --api-addr=:8888 \
  --debug-api-enable=true \
  --debug-api-addr=:6666
```

### Configuration file
Bee can also be configured by providing a yaml configuration file using the `--config` flag.

```console
bee start --config ~/bee-config.yaml 
```

:::tip
Run `bee printconfig &> bee-default.yaml` to print a default version of the configuration file.
:::


### Automatically generate a config file

Configuration files can be easily generated tby simply substituting the `start` command with `printconfig` when starting Bee using the command line.

#### Example

Here we substitute `start` for `printconfig` when specifying arguments at the command line.

```console
bee printconfig \
  --verbosity=5 \
  &> bee-config.yaml
```

This produces the following file contents, showing the default configuration of Bee, with some added log verbosity:

```yaml
api-addr: :8080
bootnode:
- /dnsaddr/bootnode.ethswarm.org
config: /Users/sig/.bee.yaml
cors-allowed-origins: []
data-dir: /Users/sig/.bee
db-capacity: "5000000"
debug-api-addr: :6060
debug-api-enable: false
global-pinning-enable: false
help: false
nat-addr: ""
network-id: "1"
p2p-addr: :7070
p2p-quic-enable: false
p2p-ws-enable: false
password: ""
password-file: ""
payment-threshold: "100000"
payment-tolerance: "10000"
tracing-enable: false
tracing-endpoint: 127.0.0.1:6831
tracing-service-name: bee
verbosity: "5"
welcome-message: ""
```

## Configuration Options

Bee provides the following options to customise your node.

#### --api-addr

*default* :8080

The ip and port the API will serve http requests from. Ommiting the IP part of the address will cause the server to listen to all requests.

#### --bootnode

*default* `/dnsaddr/bootnode.ethswarm.org`

This is a [multiaddr](https://github.com/multiformats/multiaddr) specifying the Bee bootnodes used for bootstrapping the network, it can be multiple values. By default a node connects to the Swarm mainnet. 

When using a private or test network, network specific bootnodes must be set. 

Any Bee node a network can act as a bootnode.

#### --config

*default* `/home/<user>/.bee.yaml`

The location of a yaml configuration file containing configuration instructions. See [configuration](#configuration-file).

#### --cors-allowed-origins

*default* `[]`

Http origin domains or wildcards defining these, which the API will allow responses to, e.g.

```console
$ bee start --cors-allowed-origins="*"
$ bee start --cors-allowed-origins="https://website.ethswarm.org"
```

#### --data-dir

*default* `/home/<user>/.bee`

The location on your disk where Bee stores it's data. This consists of three types of data.

##### 1. Chunk Data

This consists of chunks and files that you have pinned locally, cached chunks you have requested, or chunks within your radius of responsibility which you are responsible for serving to your peers.

##### 2. State Data

This is information about the local state of your Bee node.

##### 3. Keystore Data

These files contain encrypted versions of your private key and should be backed up and kept private.

:::danger
Keep the key files in your keystore data directory safe! 

They are the cryptographic proof of your network identity and cannot be recovered.
:::

#### --db-capacity 

*default* `5000000`

Chunk database capacity in chunks. A chunk is 4096 kb in size, so the total database capacity in kb can be estimated as `db-capacity * 4096`. The default 5,000,000 chunks is therefore approximately 20.5gb. We recommend a minimum of 2.5gb capacity for a node to be able to effectively function in the network. Light nodes that do not participate in sharing may be able to specify less.

#### --debug-api-addr

*default* `:6060`

The IP and port the [Debug API](/api-reference/debug-api) will serve http requests from. 

Ommiting the IP part of the address will cause the server to listen to all requests.

`--debug-api-enable` must be set to `true`.

#### --debug-api-enable

*default* `false`

Set this to `true` to enable access to the [Debug API](/api-reference/debug-api)

#### --global-pinning-enable

*default* `false`

Enables the [Global Pinning](/something) functionality when set to `true`.

#### --nat-address

*default* `""`

#### --network-id

*default* `1`

#### --p2p-addr

*default* `:7070`


#### --p2p-quic-enable

*default* `false`

#### --p2p-ws-enable

*default* `false`

#### --password

*default* `""`

The password to decrypt keys. 

:::danger
Passing passwords as command line arguments is insecure. Use a password file or environment variables in production environments.
:::

#### --password-file

*default* `""`

The path to a file that contains password for decrypting keys. The empty string assumes no file is presented.

#### --verbosity

*default* `info`

0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=trace

#### --welcome-message

*default* `""`

Custom welcome message to be displayed to peers on succesful connection.

<!-- payment-threshold: "100000"
payment-tolerance: "10000"
tracing-enable: false
tracing-endpoint: 127.0.0.1:6831
tracing-service-name: bee -->


### Environment variables

Bee config may also be passed using environment variables.

Environment variables are set as variables in your operating systems session or systemd configuration file. To set an environment variable, type the following in your terminal session.

```sh
$ export VARIABLE_NAME=variableValue
```

Verify if it is correctly set by running `echo $VARIABLE_NAME`.

All available configuration options are also available as captilaised and underscored environment variables.

e.g. `--api-addr` becomes `BEE_API_ADDR`.

### Precedence Order of Configuration

Configuration is processed in the following ascending priority order of preference:

1. Command Line Variables
2. Environment Variables
3. Configuration File
