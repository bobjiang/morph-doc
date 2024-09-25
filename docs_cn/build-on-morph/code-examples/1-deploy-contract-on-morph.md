---
title: 在 Morph 上部署合约
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---




Morph Holesky 测试网允许任何人在 Morph 上部署智能合约。本教程将指导您使用常见的以太坊开发工具在 Morph Holesky 上部署合约。

这[demo repo](https://github.com/morph-l2/morph-examples/tree/main/contract-deployment-demos)说明了合同部署[Hardhat](https://hardhat.org/)和[Foundry](https://github.com/foundry-rs/foundry).

:::tip
在开始部署合约之前，您需要从 Holesky faucet 请求测试代币并使用
[bridge](https://bridge-holesky.morphl2.io)将一些测试 ETH 从 _Holesky_ 转移到 _Morph Holesky_。

看看我们的[Faucet](../../quick-start/3-faucet.md)了解详情。
:::

<!--

## Deploy contracts with Remix

-->


## Deploy with Hardhat

### Clone the repo

```bash
git clone https://github.com/morph-l2/morph-examples.git
```

### Install Dependencies

如果您还没有安装，请安装[nodejs](https://nodejs.org/en/download/)和[yarn](https://classic.yarnpkg.com/lang/en/docs/install).

```bash
cd contract-deployment-demos/hardhat-demo
yarn install
```
这将为您安装所需的一切，包括安全帽。


### Compile

编译你的合同

```bash
yarn compile
```

### Test

这将运行 test/Lock.ts 中的测试脚本

```bash
yarn test
```

### Deploy

创建一个`.env`遵循示例的文件`.env.example`在根目录中。改变`PRIVATE_KEY`到您自己的帐户私钥`.env`.

 And Change the network settings in the hardhat.config.ts file with the following information:

```javascript
    morphTestnet: {
      url: process.env.MORPH_TESTNET_URL || "",
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
    }
   ```
然后运行以下命令在 Morph Holesky 测试网上部署合约。这将运行设置初始参数的部署脚本，您可以在scripts/deploy.ts中编辑脚本

```bash
yarn deploy:morphTestnet
```

### Verify your contracts on Morph Explorer

To verify your contract through hardhat, you need to add the following Etherscan and Sourcify configs to your hardhat.config.js file:

```javascript
module.exports = {
  networks: {
    morphTestnet: { ... }
  },
  etherscan: {
    apiKey: {
      morphTestnet: 'anything',
    },
    customChains: [
      {
        network: 'morphTestnet',
        chainId: 2810,
        urls: {
          apiURL: 'https://explorer-api-holesky.morphl2.io/api? ',
          browserURL: 'https://explorer-holesky.morphl2.io/',
        },
      },
    ],
  },
};
```
然后运行hardhat verify命令完成验证

```bash
npx hardhat verify --network morphTestnet DEPLOYED_CONTRACT_ADDRESS <ConstructorParameter>
```

例如

```bash
npx hardhat verify --network morphTestnet 0x8025985e35f1bAFfd661717f66fC5a434417448E '0.00001'
```


成功后，您可以在上面查看您的合约和部署交易[Morph Holesky Explorer](https://explorer-holesky.morphl2.io)


## Deploy contracts with Foundry

### Clone the repo

```bash
git clone https://github.com/morph-l2/morph-examples.git
```

### Install Foundry
```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

Then go the right folder of our example:

```bash
cd contract-deployment-demos/foundry-demo
```

### Compile

```bash
forge build
```
### Deploy

已经为您设置了部署脚本和环境变量的使用。您可以在 script/Counter.s.sol 查看脚本

将您的 .env.example 文件重命名为 .env 并填写您的私钥。 RPC URL 已与验证者 URL 一起填写。

To use the variables in your .env file run the following command: 

```shell
source .env
```

You can now deploy to Morph with the following command: 

```shell
forge script script/Counter.s.sol --rpc-url $RPC_URL --broadcast --private-key $DEPLOYER_PRIVATE_KEY --legacy
```

根据需要调整您自己的脚本名称。

### Verify 

Verification requires some flags passed to the normal verification script. You can verify using the command below:

```bash
 forge verify-contract YourContractAddress Counter\
  --chain 2810 \
  --verifier-url $VERIFIER_URL \
  --verifier blockscout --watch
```

成功后，您可以在上面查看您的合约和部署交易[Morph Holesky Explorer](https://explorer-holesky.morphl2.io).


## Questions and Feedback

感谢您参与 Morph Holesky 测试网并进行开发！如果您遇到任何问题，请加入我们[Discord](https://discord.com/invite/L2Morph)并找到我们#dev-support channel.


