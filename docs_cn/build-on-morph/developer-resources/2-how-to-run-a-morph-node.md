---
title: 如何运行变形节点
lang: zh-CN
---


## Run a Morph Full Node 

本指南概述了启动 Morph 节点的步骤。该示例假设主目录是`~/.morph`

### Hardware requirements

运行变形节点需要 2processes:`geth`和`node`.

-`Geth`:theMorph执行层需要满足[go-ethereum hardware requirements](https://github.com/ethereum/go-ethereum#hardware-requirements)但存储空间较小，到目前为止 500GB 就足够了。

-`Node`:theMorph共识层嵌入tendermint，需要满足[tendermint hardware requirements](https://docs.tendermint.com/v0.34/tendermint-core/running-in-production.html#processor-and-memory).


:::tip
由于当前 geth 实现的限制，仅支持归档模式，这意味着存储大小将随着生成的块而不断增加。
:::

### Build executable binary

#### Clone morph

```
mkdir -p ~/.morph 
cd ~/.morph
git clone https://github.com/morph-l2/morph.git
```

目前，我们使用标签 v0.2.0-beta 作为我们的测试版本。

```
cd morph
git checkout v0.2.0-beta
```

#### Build Geth

Notice: You need C compiler to build geth

```
make nccc_geth
```

#### Build Node

```
cd ~/.morph/morph/node 
make build
```

### Sync from genesis block

#### Config Preparation

下载配置文件并创建数据目录

```
cd ~/.morph
wget https://raw.githubusercontent.com/morph-l2/config-template/main/holesky/data.zip
unzip data.zip
```

与节点创建共享秘密

```
cd ~/.morph
openssl rand -hex 32 > jwt-secret.txt
```

#### Script to start the process

*盖斯*

```
./morph/go-ethereum/build/bin/geth --morph-holesky \
    --datadir "./geth-data" \
    --http --http.api=web3,debug,eth,txpool,net,engine \
    --authrpc.addr localhost \
    --authrpc.vhosts="localhost" \
    --authrpc.port 8551 \
    --authrpc.jwtsecret=./jwt-secret.txt \
    --miner.gasprice="100000000" \
    --log.filename=./geth.log
```

*tail -f geth.log* 检查Geth是否正常运行，或者您也可以执行下面的curl命令来检查您是否连接到对等点。

```
curl -X POST -H 'Content-Type: application/json' --data 
'{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}' 
localhost:8545

{"jsonrpc":"2.0","id":74,"result":"0x3"}
```


*节点*

```
./morph/node/build/bin/morphnode --home ./node-data \
     --l2.jwt-secret ./jwt-secret.txt \
     --l2.eth http://localhost:8545 \
     --l2.engine http://localhost:8551 \
     --log.filename ./node.log
```

tail -f node.log 检查节点是否正常运行，也可以执行命令curl检查节点连接状态。

```
curl http://localhost:26657/net_info

{
  "jsonrpc": "2.0",
  "id": -1,
  "result": {
    "listening": true,
    "listeners": [
      "Listener(@)"
    ],
    "n_peers": "3",
    "peers": [
      {
        "node_info": {
          "protocol_version": {
            "p2p": "8",
            "block": "11",
            "app": "0"
          },
          "id": "0fb5ce425197a462a66de015ee5fbbf103835b8a",
          "listen_addr": "tcp://0.0.0.0:26656",
          "network": "chain-morph-holesky",
          "version": "0.37.0-alpha.1",
          "channels": "4020212223386061",
          "moniker": "morph-dataseed-node-1",
          "other": {
            "tx_index": "on",
            "rpc_address": "tcp://0.0.0.0:26657"
          }
        },
        "is_outbound": true,
```

### Check sync status


卷曲http://localhost:26657/status检查节点的同步状态

```
{
  "jsonrpc": "2.0",
  "id": -1,
  "result": {
    "node_info": {
      "protocol_version": {
        "p2p": "8",
        "block": "11",
        "app": "0"
      },
      "id": "b3f34dc2ce9c4fee5449426992941aee1e09670f",
      "listen_addr": "tcp://0.0.0.0:26656",
      "network": "chain-morph-holesky",
      "version": "0.37.0-alpha.1",
      "channels": "4020212223386061",
      "moniker": "my-morph-node",
      "other": {
        "tx_index": "on",
        "rpc_address": "tcp://0.0.0.0:26657"
      }
    },
    "sync_info": {
      "latest_block_hash": "71024385DDBEB7B554DB11FD2AE097ECBD99B2AF826C11B2A74F7172F2DEE5D2",
      "latest_app_hash": "",
      "latest_block_height": "2992",
      "latest_block_time": "2024-04-25T13:48:27.647889852Z",
      "earliest_block_hash": "C7A73D3907C6CA34B9DFA043FC6D4529A8EAEC8F059E100055653E46E63F6F8E",
      "earliest_app_hash": "",
      "earliest_block_height": "1",
      "earliest_block_time": "2024-04-25T09:06:30Z",
      "catching_up": false
    },
    "validator_info": {
      "address": "5FB3D3734640792F14B70E7A53FBBD39DB9787A8",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "rzN67ZJWsaLSGGpNj7HOWs8nrL5kr1n+w0OckWUCetw="
      },
      "voting_power": "0"
    }
  }
}
```

返回的“捕捉_up”指示节点是否同步。 True 表示它是同步的。同时，返回的latest_block_height表示该节点同步的最新区块高度。



