## Haidai Testnets

This repo collects the genesis and configuration files for the various `haidai`
testnets. It exists so the [Haidai Network](https://github.com/haidainetwork/haidai)
does not get bogged down with large genesis files and status updates


## Testnet Status

🚀 Latest testnet: [haidai-testnet-xia](./xia) 

- 2021-03-22T03:40:03.791687Z - [haidai-testnet-xia](./xia) 

## Join the Public Testnet

- Connect smart contract to the Web3 world!


**Download testnet file**

```
git clone https://github.com/haidainetwork/testnets.git
```

**Reset Data**

```
rm $HOME/.haidaid/config/config.toml $HOME/.haidaid/config/genesis.json

haidaid unsafe-reset-all
```

Your node is now in a pristine state while keeping the original `priv_validator.json` and `config.toml`. If you had any sentry nodes or full nodes setup before, your node will still try to connect to them, but may fail if they haven't also been upgraded.

***⚠️ Warning***

Make sure that every node has a unique `priv_validator.json`. Do not copy the `priv_validator.json` from an old node to multiple new nodes. Running two nodes with the same `priv_validator.json` will cause you to `double sign`.

**Init with haidaid**

```
haidaid init {your_name} --overwrite --chain-id haidai-testnet-xia
```

**Software Upgrade**

```
cp genesis.json config.toml $HOME/.haidaid/config/

haidaid start
```

***🏷️NOTE***

If you have issues at this step, please check that you have the latest stable version of testnets.

**Chain sync**

After haidaid start, you will connect to testnet, and you will see blow

```
8:35PM INF starting ABCI with Tendermint
8:35PM INF Starting multiAppConn service impl=multiAppConn module=proxy
8:35PM INF Starting localClient service connection=query impl=localClient module=abci-client
8:35PM INF Starting localClient service connection=snapshot impl=localClient module=abci-client
8:35PM INF Starting localClient service connection=mempool impl=localClient module=abci-client
8:35PM INF Starting localClient service connection=consensus impl=localClient module=abci-client
8:35PM INF Starting EventBus service impl=EventBus module=events
8:35PM INF Starting PubSub service impl=PubSub module=pubsub
```

**Config with Haidai**

- `$HOME/.haidaid/config/app.toml` - Haidai Network config

- `$HOME/.haidaid/config/config.toml` - Tendermint config


**Explore Haidai Network**

```
haidaid help
```

**Documentation**

Documentation for the Haidai Network lives at [docs.haidai.one](https://docs.haidai.one)


**Talk to us!**

We have active, helpful communities on Twitter, Discord, and Telegram.

- [Twitter](https://twitter.com/haidainetwork/)
- [Telegram](https://t.me/haidainetwork)


#### Testnets Roadmap


**2021-03-22T03:40:03.791687Z Testnet Xia(夏朝)**

- Released v1.0 with update for Tendermint v0.38.4 and Cosmos-sdk v0.42.2
- Please update to this to sync with the testnet


