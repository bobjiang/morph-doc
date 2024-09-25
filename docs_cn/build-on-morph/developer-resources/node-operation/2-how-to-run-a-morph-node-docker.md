---
title: 使用 Docker 运行 Morph 全节点
lang: zh-CN
---


本指南将帮助您启动在 docker 容器中运行的完整节点。

## Quick Start

目前，用户需要使用我们提供的 Docker 文件和 Docker Compose 文件自行构建 Docker 镜像。不过，无需担心，只需一条命令即可快速启动全节点。该命令将为您处理一切，包括下载快照、结构数据和配置文件、构建映像以及启动容器。

1.克隆dockerfile存储库

```bash
git clone --branch release/v0.2.x https://github.com/morph-l2/morph.git
```
2. 运行以下命令

```bash
cd ops/publicnode
make run-holesky-node
```

运行此命令将创建一个`.morph-holesky` directory in your user directory by default, serving as the node's home directory. Before starting the node, this command will perform several preparations:

- 创建节点的主目录并将默认配置文件复制到其中。
- 准备`secret-jwt.txt`文件用于在 geth 和节点之间的 RPC 调用期间进行身份验证。
- 下载最新快照数据，加速节点同步。
- 将提取的快照数据放入主目录中的相应文件夹中。

完成这些准备工作后，该命令将自动构建镜像并启动容器，并将 Docker 卷挂载到创建的节点主目录。

:::info
如果这是您第一次运行，这些过程可能需要一些时间。请注意，如果您是第一次启动节点但已经有一个`.morph-holesky`目录，您必须在运行该命令之前删除该目录。否则，准备阶段将被跳过，这可能会导致节点无法正常运行。

如果命令执行失败，还需要删除之前创建的`.morph-holesky`重新启动之前的目录。
:::

## Advanced Usage

随着[Quick Start](#quick-start)通过上面的指导，您可以使用默认配置文件快速启动节点。不过，我们也支持自定义节点的主目录和参数设置。

### Customizing Data Directory
Docker容器挂载的主机目录路径在```ops/publicnode/.env```文件。

```js title="ops/publicnode/.env"
// the home folder of your Morph node
NODE_HOME=${HOME}/.morph-holesky 
// the data directory for your execution client: geth
GETH_DATA_DIR=${NODE_HOME}/geth-data
// the data directory for you consensus client: tendermint
NODE_DATA_DIR=${NODE_HOME}/node-data
// the entrypoint shell script for start execution client
GETH_ENTRYPOINT_FILE=${NODE_HOME}/entrypoint-geth.sh
// the jwt secret file for communicating between execution client and consensus client via engine API
JWT_SECRET_FILE=${NODE_HOME}/jwt-secret.txt
// the snapshot name for holesky Morph node 
SNAPSHOT_NAME=snapshot-20240805-1
```

您可以根据需要灵活地自定义目录路径。
请注意，如果要执行 **make run-holesky-node** 生成运行节点所需的配置文件和快照，则需要确保指定的节点主目录是新的（不是之前创建的）并执行**不**改变路径```GETH_DATA_DIR```和```NODE_DATA_DIR```.

### Customizing parameters

节点启动所需的默认配置位于```ops/publicnode/holesky```目录。如果你的节点主目录为空，**run**命令会自动将这些配置文件复制到节点的docker容器中挂载的目录中。

```javascript
└── holesky
    ├── entrypoint-geth.sh
    ├── geth-data
    │   └── static-nodes.json
    └── node-data
        ├── config
        │   ├── config.toml
        │   └── genesis.json
        └── data
```

如果您想修改 Geth 启动命令，可以通过编辑```entrypoint-geth.sh```文件。对于Tendermint相关配置参数的调整，您应该修改node-data/config/config.toml文件。
请注意，如果您已自定义```GETH_DATA_DIR```和```NODE_DATA_DIR```，您需要手动将修改后的配置文件放置在适当的位置。
#### Managing Snapshots Yourself

您还可以手动管理快照，特别是当您使用节点目录的自定义路径时。
**make download-and-decompress-snapshot** 命令在```ops/publicnode```目录将帮助您下载和解压缩快照存档。

然后，您需要手动将解压后的数据文件放置到相应的节点数据目录中。
例如，如果快照文件夹名为```snapshot-20240805-1```，将内容移出```snapshot-20240805-1/geth```到```${GETH_DATA_DIR}/geth```目录和内容来自```snapshot-20240805-1/data```到```${NODE_DATA_DIR}/data```目录。