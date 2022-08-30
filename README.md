# Plugchain Mainnet

## Overview

The current plugchaind Version of the Plugchain Hub mainnet is [`v1.0.0`](https://github.com/oracleNetworkProtocol/plugchain/releases/tag/v1.0.0).

For a full set of instructions on boostrapping a mainnet node, see the Hub's [**Join the Plugchain Hub Mainnet**](https://oraclenetworkprotocol.github.io/plugchain/get-started/mainnet.html) documentation.

## Quickstart

**Preresquisites**
- `make` & `gcc`
- `Go 1.16+`

> **Note**: Make sure to have all prerequisites installed. See the [installation docs](https://oraclenetworkprotocol.github.io/plugchain/get-started/install.html) for clarification and a detailed set of instructions.

**State Sync**

To enable state sync, visit an [explorer](https://www.plugchain.network/v2/blockList) to get a recent block height and corresponding hash. A node operator can choose any height/hash in the current bonding period, but as the recommended snapshot period is 1000 blocks, it is advised to choose something close to current height - 1000. Set these parameters in the code snippet below `<BLOCK_HEIGHT>` and `<BLOCK_HASH>`

```bash
# Build plugchaind binary and initialize chain
cd $HOME
git clone -b v1.0.0 https://github.com/oracleNetworkProtocol/plugchain
cd plugchain
make install
plugchaind version

plugchaind init myNode --chain-id plugchain_520-1

# Prepare genesis file for plugchain_v1
curl -o $HOME/.plugchain/config/genesis.json https://raw.githubusercontent.com/oracleNetworkProtocol/mainnet/main/version/v1/genesis.json
curl -o $HOME/.plugchain/config/app.toml https://raw.githubusercontent.com/oracleNetworkProtocol/mainnet/main/version/v1/app.toml
curl -o $HOME/.plugchain/config/config.toml https://raw.githubusercontent.com/oracleNetworkProtocol/mainnet/main/version/v1/config.toml
curl -o $HOME/.plugchain/config/client.toml https://raw.githubusercontent.com/oracleNetworkProtocol/mainnet/main/version/v1/client.toml

# Configure State sync
# cd $HOME/.plugchain/config
# sed -i 's/enable = false/enable = true/' config.toml
# sed -i 's/trust_height = 0/trust_height = <BLOCK_HEIGHT>/' config.toml
# sed -i 's/trust_hash = ""/trust_hash = "<BLOCK_HASH>"/' config.toml
# sed -i 's/rpc_servers = ""/rpc_servers = ""/' config.toml

#Start plugchain
plugchaind start 
```

Next, your node will perform all chain upgrade procedures. Between each upgrade, you must sync blocks with a specific version. Don't worry about using an older version at an upgrade height, the node will stop automatically.

| Proposal | Starting Height | Upgrade Height | plugchaind Version |
| -------- | ------------ | -------------- | ----- |
| [v1.0](https://www.plugchain.network/v2/communityDetail?id=7)  |  3000000     |    | [v1.1.0](https://github.com/oracleNetworkProtocol/plugchain/releases/tag/v1.1.0) |
| [v1.2.1](https://www.plugchain.network/v2/communityDetail?id=8)  |  3349542     |  3576853  | [v1.2.1](https://github.com/oracleNetworkProtocol/plugchain/releases/tag/v1.2.1) |
| [v1.5.0](https://www.plugchain.network/v2/communityDetail?id=9)  |  3935641     |  4152263  | [v1.5.0](https://github.com/oracleNetworkProtocol/plugchain/releases/tag/v1.5.0) |
| [v1.7.0](https://www.plugchain.network/v2/communityDetail?id=10)  |  5420512     |  5633000  | [v1.7.0](https://github.com/oracleNetworkProtocol/plugchain/releases/tag/v1.7.0) |

## Upgrade to Validator Node

You now have an active full node. What's the next step? You can upgrade your full node to become a Plugchain Validator. The top 50 validators have the ability to propose new blocks to the Plugchain Hub. Continue onto [the Validator Setup](https://oraclenetworkprotocol.github.io/plugchain/zh/get-started/mainnet.html#%E5%8D%87%E7%BA%A7%E4%B8%BA%E9%AA%8C%E8%AF%81%E4%BA%BA%E8%8A%82%E7%82%B9).
