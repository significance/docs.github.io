---
title: Start Your Node
id: start-your-node
---

Run `bee start`. This command starts your bee node with all configuration parameters on their default value.


There are many ways to customise and interact with your Bee node. For a full list, check out the [configuration guide](/installation/configuration), or simply run your Bee terminal command with the `--help` flag, eg. `bee start --help` or `bee --help`.

## Enter your password

When you first run Bee, you will be prompted to input a user password. It is important to choose a strong unique password, as this protects your valuable **private key** which is generated during startup. This 32 byte secret code is stored encrypted in the `--data-dir` on the computer running your node (default `~/.bee`). It represents your Overlay Address - your anonymous identity in Swarm.

```

Welcome to the Swarm.... Bzzz Bzzzz Bzzzz
                \     /
            \    o ^ o    /
              \ (     ) /
   ____________(%%%%%%%)____________
  (     /   /  )%%%%%%%(  \   \     )
  (___/___/__/           \__\___\___)
     (     /  /(%%%%%%%)\  \     )
      (__/___/ (%%%%%%%) \___\__)
              /(       )\
            /   (%%%%%)   \
                 (%%%)
                   !
Password:
```

If all goes well, you should see your node automatically start to connect to other Bee nodes all over the world. Your node will begin to request chunks of data that fall within your *radius of responsibilty* - data that you will serve to the rest of the swarm. You will then begin to serve requests for these chunks from other peers, for which you will soon be rewarded in BZZ.

:::tip Incentivisation
In the swarm, storing and serving other nodes chunks of data earns you rewards! When you help to store and distribute data, you will be rewarded with cryptographic tokens that you can then be used to consume interesting content in Swarm. Check out (accounting)[] for a sneak peek at the exciting incentivisation features coming soon in Swarm 1.0!
:::

Your Bee client has now generated an elliptic curve keypair similar to a Bitcoin or Ethereum wallet. There are stored in your data directory, in the `keys` folder. You can find your data directory using the `bee printconfig` command.

:::danger Keep Your Keys and Password Safe!
Your keys and password are very important, back these files up and store them in a secure place that only you have access to. With great privacy comes great responsibility - while no-one will ever be able to guess your key, but you will not be able to recover them if you lose them either, so be sure to look after them well and keep secure backups.
:::


## Getting help
The CLI has documentation build-in. Running `bee` gives you an entry point to the documentation. Running `bee start -h` or `bee start --help` will tell you how you can configure you bee node via the command line arguments.
