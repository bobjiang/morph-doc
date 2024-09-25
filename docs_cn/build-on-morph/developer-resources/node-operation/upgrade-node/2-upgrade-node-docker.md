---
title: 升级从 docker 运行的节点
lang: zh-CN
---


如果您使用自定义设置为节点运行 Docker 容器，则需要自行更新 docker 映像，然后重新启动容器。

源代码位于https://github.com/morph-l2/morph.git.您需要切换到最新版本的代码，然后更新您的 docker 镜像。

如果您正在使用[Run a Morph node with docker](../2-how-to-run-a-morph-node-docker.md)启动docker容器后，可以按照后续步骤升级节点。

### Step1:  Fetch latest code version 
```bash
git clone https://github.com/morph-l2/morph.git
## checkout the latest version of the source code you need
git checkout ${latestVersion}
```
### Step2: Stop the nodes and delete previous images

```bash
## stop docker container
cd ops/publicnode
make stop-holesky-node
make rm-holesky-node
## delete the pervious docker image for node
docker rmi morph/node:latest
## delete the pervious docker image for geth
docker rmi morph/geth-nccc:latest
```

### Step3: Build the latest image and restart the container

:::note
请注意，我们需要确保Docker容器的启动参数与之前使用的一致。如果您之前使用过自定义配置，请确保本次运行中使用的配置和目录路径与之前相同。详情请参阅[**Advanced Usage**](../2-how-to-run-a-morph-node-docker.md#advanced-usage)
:::

```bash
## start the docker container, it will automatically build the new docker images
make run-holesky-node
```

