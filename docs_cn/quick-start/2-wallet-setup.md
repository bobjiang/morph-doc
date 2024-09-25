---
title: 钱包设置
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


## Wallet

要与 Morph 上的 dApp 交互，您需要一个兼容的钱包。以下是一些钱包示例和配置提示。

<!--
### Bitget Wallet

TBD
-->

### MetaMask

- 安装：MetaMask 可以从其 [官方网站](https://metamask.io/download/) 安装。
- 导入配置：要为 Morph Testnet 设置 MetaMask，请单击 [https://explorer-holesky.morphl2.io/](Morph Holesky 区块浏览器页面) 上的“添加到钱包”按钮。这将自动导入 Morph 测试网的链 ID 和 RPC URL。
- 使用以太坊 Holesky 测试网：Morph Testnet 使用以太坊 Holesky 测试网作为其底层 L1，默认情况下已在 MetaMask 中配置。要访问它，请在 MetaMask 网络选择下拉菜单中启用“显示/隐藏测试网络”。

### 手动网络配置

目前，“添加到钱包”链接可能尚未与所有钱包兼容。如果您在使用它们时遇到问题，您可能需要通过插入下表中的配置详细信息来手动添加 Holesky Testnet 和 Morph：


#### Network Configuration


|名称 | RPC URL |链ID |区块浏览器 |符号|
| -------- | -------------------------- | ------------- | ---------- | ------------------------------------ |
| Morph Holesky 测试网 |https://rpc-quicknode-holesky.morphl2.io| 2810    |https://explorer-holesky.morphl2.io|以太币 |
|以太坊霍尔斯基 |https://ethereum-holesky-rpc.publicnode.com/| 17000    |https://holesky.etherscan.io|以太币 |


您还可以访问[chainlist](https://chainlist.org/?chain=11155111&search=morph&testnets=true)添加 Morph 测试网和以太坊测试网。