---
title: 升级主机上运行的节点
lang: zh-CN
---


升级节点很简单。只需安装新版本的节点可执行文件并替换以前的版本即可。然后，停止当前正在运行的节点并使用更新的版本重新启动它。节点将自动使用您旧节点的数据并同步您关闭旧软件后挖掘的最新块。

Running the node requires two binary files: `morphnode`和`geth`。根据您的具体需要选择升级二进制文件。

### Step1: Compile the new version of the code

```bash
git clone https://github.com/morph-l2/morph.git
## checkout the latest version of the source code you need
git checkout ${latestVersion}
## install geth
make nccc_geth
## install morphnode
cd ./morph/node && make build
```

### Step2: Stop nodes

```bash
## stop morphnode process
pid=`ps -ef | grep morphnode | grep -v grep | awk '{print $2}'`
kill  $pid

## stop geth process
pid=`ps -ef | grep geth | grep -v grep | awk '{print $2}'`
kill  $pid
```

### Step3: Restart

确保使用升级前相同的启动命令

```bash
## start geth
./morph/go-ethereum/build/bin/geth --morph-holesky \
    --datadir "./geth-data" \
    --http --http.api=web3,debug,eth,txpool,net,engine \
    --authrpc.addr localhost \
    --authrpc.vhosts="localhost" \
    --authrpc.port 8551 \
    --authrpc.jwtsecret=./jwt-secret.txt \
    --log.filename=./geth.log

## start geth    
./morph/node/build/bin/morphnode --home ./node-data \
     --l2.jwt-secret ./jwt-secret.txt \
     --l2.eth http://localhost:8545 \
     --l2.engine http://localhost:8551 \
     --log.filename ./node.log 
```