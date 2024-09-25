---
title: 开发设置
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


# Start Developing on Morph

在 Morph 上进行开发与在以太坊上进行开发一样简单。

要将合约部署到 MorphL2 链上，只需设置目标 MorphL2 链的 RPC 端点并使用您喜欢的以太坊开发框架进行部署：


-[Hardhat](https://hardhat.org/)
-[Foundry](https://github.com/foundry-rs/foundry)
-[Brownie](https://eth-brownie.readthedocs.io/en/stable/)
-[Alchemy](https://docs.alchemy.com/reference/alchemy-sdk-quickstart)
-[QuickNode SDK](https://www.quicknode.com/docs/quicknode-sdk/getting-started?utm_source=morph-docs)

...一切正常！


# Holesky Testnet:

## Step 1: Network Configuration

开始之前, 确保使用以下的网络:

|网络名称 | Morph Holesky 测试网 | Holesky 测试网 |
| --- | --- | --- |
| RPC URL |https://rpc-quicknode-holesky.morphl2.io|https://ethereum-holesky-rpc.publicnode.com/|
|链ID | 2810 | 2810 17000 |
|货币符号|以太币 |以太币 |
|块资源管理器 URL |https://explorer-holesky.morphl2.io/|https://holesky.etherscan.io/|

:::tipWebsocket 连接

wss://rpc-quicknode-holesky.morphl2.io

:::

### Tendermint Consensus Information

Tendermint RPC: https://rpc-consensus-holesky.morphl2.io

Tendermint RPC Documentation: https://docs.tendermint.com/v0.34/rpc/#/


## Step 2: Set up your developing framework

### Hardhat

修改 Hardhat 配置文件 Hardhat.config.ts 以指向 Morph 公共 RPC。

```jsx
const config: HardhatUserConfig = {
  ...
  networks: {
    morphl2: {
      url: 'https://rpc-quicknode-holesky.morphl2.io',
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
      gasprice = 2000000000
    },
  },
};

```

### Foundry

To deploy using Morph Public RPC, run:

```jsx
forge create ... --rpc-url= --legacy
```



### ethers.js

Setting up a Morph  provider in an ethers script:

```jsx
import { ethers } from 'ethers';

const provider = new ethers.providers.JsonRpcProvider(
  'https://rpc-quicknode-holesky.morphl2.io'
);
```

## Step 3: Acquire Ether

要开始在 Morph 上构建，您可能需要一些测试网 ETH。使用水龙头获取holesky Ether，然后[bridge](https://bridge-holesky.morphl2.io)Morph 测试网的测试以太坊 Ether。

每个水龙头都有自己的规则和要求，因此您可能需要尝试一些才能找到适合您的水龙头。

Holesky ETH faucet websites:

https://stakely.io/en/faucet/ethereum-holesky-testnet-eth

https://faucet.quicknode.com/ethereum/holesky

https://holesky-faucet.pk910.de/

https://cloud.google.com/application/web3/faucet/ethereum（需要一个谷歌帐户）

我们有自己的[website faucet](https://morphfaucet.com/)可以为您首次使用索取 ETH 和 USDT。


Morph还提供了[Discord faucet](../../quick-start/3-faucet.md#morph-holesky-eth)获取Morph Holesky USDT & Morph Holesky ETH。

一旦您在 Holesky 上收到 ETH，您应该会在 *Holesky 网络* 上的钱包中看到它。它们可能需要几秒钟的时间才会显示，但您可以通过在**上查找发送到您地址的交易来检查状态[Holesky Block Explorer](https://holesky.etherscan.io/)**.


