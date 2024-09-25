---
title: 交易生命周期
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


## How is a L2 transaction processed on Morph

1. 提交交易

用户发起的交易首先发送到 L2 节点的内存池，在那里等待排序器的选择和处理。


2. 交易共识

在排序器网络内，交易经历共识过程。选定的排序器提出包含交易的块，然后将块发送到共识层（共识客户端）。

然后其他定序器通过执行该块来验证该块，从而有效地验证交易的合法性。


3. 交易执行

一旦该区块的所有投票最终确定，每个定序器和节点将应用该区块来更新其本地状态。

4. 交易批量

当达到批次点时，每个定序器将需要构建上一个 epoch 共识的所有区块的批次，该批次将通过要求每个定序器签名来达成共识，所有签名将与 BLS 签名聚合。

5. 批量测序

这[selected sequencer](../general-protocol-design/1-rollup.md)将把批次提交给 Layer 1 Rollup 合约以进行验证并确保数据可用性。

6. 批量验证

一个批次（批次内的交易也是如此）首先会经过 Rollup 合约的 BLS 签名验证，确认 L2 共识结果，然后一个批次会经过[challenge period](../3-optimistic-zkevm.md)被标记为最终确定，巩固其在 L1 和 L2 状态中的地位。

## Morph Transaction Status

### Processing​

一旦提交，交易就会进入由排序器管理的共识阶段，并被放入区块预执行中。

### Confirmed​

由 Sequencer 执行后，事务的更新状态是 L2 本地的。然后将其分批发送到 L1，在最终确定之前必须经历挑战期。

### Safe

包含交易的批次已提交到第 1 层，但尚未最终确定。

### Finalized​

交易在经过挑战期或通过零知识证明（ZK-Proof）验证后被视为已完成。只有这样才正式融入最终的L1和L2状态。
