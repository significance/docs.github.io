---
title: Working With Your Node
id: working-with-your-node
---

Now that you have created your Swarm identity and your node has begun to participate in the global p2p swarm network we can take a closer look at what's happening.

### Debug API

The [Debug API](/api-reference/debug-api) provides a privileged environment where you can get more information about what's going on with your Bee node.

To enable the Debug API we must pass a configuration flag into our `bee start` command as it is disabled by default.

```sh
$ bee start --debug-api-enable --debug-api-addr=localhost:6060
```

:::info
Here we've specified that the debug api should run only on *localhost*, for added security.
:::

#### Checking Connectivity

First, let's check how many nodes we are currently connected to.

```sh
curl -s http://localhost:6060/peers | jq '.peers | length'
23
```

Great, we're currently connected and sharing data with 23 other nodes!

:::info
Here we're using `jq` to count the amount of objects in the `peers` array from our JSON response, learn more about `jq` [here](https://stedolan.github.io/jq/manual/#Basicfilters)
:::

#### Inspecting Network Topology

We can also gain more insight into the network your Bee client is a part of using the `topology` endpoint.

```sh
curl -X GET http://localhost:6060/health | jq
```

In this example, our node is beginning to form a healthy network. We hope to see our node adding and connected nodes in as many bins as possible. Learn more about promiximity order bins and how your Bee node becomes part of the ordered p2p network in [The Book of Swarm](/the-book-of-swarm/download).

```
{
  "baseAddr": "793cdae71d51b0ffc09fecd1c5b063560150cf2e1d55058bad4a659be5894ab1",
  "population": 159,
  "connected": 19,
  "timestamp": "2020-08-27T19:24:16.451187+01:00",
  "nnLowWatermark": 2,
  "depth": 4,
  "bins": {
    "bin_0": {
      "population": 77,
      "connected": 4,
      "...": "..."
    },
    "bin_1": {
    	"population": 37,
      	"connected": 4,
    	}
    }
  }
}
```

A full Debug API reference can be found [here](/api-reference/debug-api).