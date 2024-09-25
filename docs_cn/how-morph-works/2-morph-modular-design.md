---
title: 变形模块化设计
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


区块链技术的模块化设计以其提高的可组合性而闻名，已成为流行趋势。 Morph 利用这一设计原则来增强其架构和功能。

![arichitecture](../../assets/docs/protocol/archi.png)

## Overview

A modular design typically divides a Layer 1 blockchain into four core functions:

1. 共识
2、执行
3. 数据可用性
4. 定居点

Morph 将这种模块化方法应用于其第 2 层解决方案，将其分为三个主要模块，每个模块负责特定功能。


### 3 Major Morph Modules

#### Sequencer Network - Consensus & Execution


![Sequencer Network](../../assets/docs/protocol/dese/seq1.png)


Sequencer网络负责Layer 2交易的执行和共识，更多细节请参考Morph的[decentralized sequencers](../how-morph-works/decentralized-sequencers/morph-decentralized-sequencer-network).

#### Optimistic zkEVM - Settlement

![Optimistic zkEVM](../../assets/docs/protocol/resvapro/opzk.png)

状态验证确保第 2 层的状态更改在第 1 层有效。Morph 引入了 Optimistic zkEVM，这是一种结合 zk-rollups 和 optimistic rollups 进行状态验证的混合解决方案。该过程涉及称为响应有效性证明（RVP）的 Morph 创新。这种创新方法可以有效地完成并解决第 2 层交易和状态。有关更多详细信息，请参阅有关的文档[Responsive Validity Proof](../how-morph-works/optimistic-zkevm).

#### Rollup - Data Availability

![Rollup](../../assets/docs/protocol/general/rollup/rollup.png)



这[Rollup](../how-morph-works/general-protocol-design/1-rollup.md)该过程涉及将第 2 层事务和状态提交到第 1 层，以确保数据可用性。 Morph 的汇总策略通过使用 zk 证明压缩块内容来最大限度地提高效率，这有助于管理第 1 层数据可用性的成本。


### 5 Morph Roles

#### Sequencers

Sequencers play a crucial role in the network by:

- 接收第 2 层用户交易并形成区块。
- 与其他测序仪达成共识。
- 执行块并应用状态转换。
- 批处理块并将其提交给第 1 层。
- 将区块与全节点同步。
- 在受到质疑时生成有效性证明。


#### Prover

当定序器受到挑战时，证明器对于生成 zk 证明至关重要。它们同步第 2 层交易信息并生成必要的 zk 证明来验证状态更改。

#### Validator

验证者可以是任何用户，在确保排序器提交给第 1 层的状态正确性方面发挥着关键作用。他们维护一个 L2 节点来同步事务和状态更改，在识别出不正确的状态时触发挑战。

#### Nodes

节点可以更轻松地访问第 2 层事务和状态，而无需主动参与网络操作。运行 L2 节点对任何人开放，不需要许可。

#### Layer 1

每个第 2 层解决方案都依赖第 1 层区块链来实现最终结算和数据可用性。对于 Morph 来说，这个角色是由以太坊来完成的。第 1 层上的关键合约确保第 2 层交易和状态的安全性和最终性。

### 6 Morph Components

#### L2 Node​

L2 节点是 Morph 架构的核心，与各种模块和角色交互。它包括以下子组件：
- 交易管理器 (Mempool)：管理所有第 2 层交易，接受和存储用户发起的交易。
- 执行器：应用状态转换并维护第 2 层的实时状态。
- 同步器：在 L2 节点之间同步数据以恢复网络状态。

#### Batch Submitter​
Batch Submitter是sequencer的一部分，负责不断获取L2区块，将其打包成批次，并将批次组装成Layer 1交易，然后提交给Layer 1合约。

#### Consensus Client​
每个排序器运行一个共识客户端来与其他排序器达成共识。目前的设计使用 Tendermint 客户端来确保无缝集成和开发人员友好性。

#### zkEVM​
zkEVM 是 Prover 的一部分，是一个 zk 友好的虚拟机，用于为以太坊区块和状态变化生成 zk 证明。这些 zk 证明最终用于证明 L2 交易和状态的有效性。

#### Aggregators​
聚合器与 zkEVM 合作，通过聚合 zk 证明进行区块生产来降低验证 zk 证明的成本。

#### Layer 1 Contract​
以太坊上的这些合约存储第 2 层交易，执行全局状态更改，并在第 2 层和第 1 层之间桥接资产和信息。它们还管理定序器集的选举和治理，继承了以太坊的安全性。


### Integration of Components, Roles, and Modules


![modular](../../assets/docs/about/overview/modu.png)


这些组件构成了 Morph 中各种角色的基础。例如，运行 L2 节点允许一个人成为节点，而添加批量提交者和共识客户端功能则可以发挥 Sequencer 的作用。这些角色协作执行 Morph 的核心功能，创建完整且高效的汇总解决方案。