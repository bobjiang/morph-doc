---
title: Morph 的去中心化定序器网络
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---



![RVP](../../../assets/docs/protocol/dese/dseq1.jpg)


## The Importance of Decentralized Sequencers



### What is a sequencer and what does it do?

在传统的第一层区块链中，交易由工作量证明系统中的矿工或权益证明系统中的验证器节点打包和处理。这些实体通过计算挖矿的竞争性任务或通过基于质押的选举获得打包、排序和生产区块的权力。

然而，当前许多第 2 层设计采用单一角色，不受竞争或质押成本的影响，负责打包和排序所有第 2 层交易。该实体被称为“定序器”。它的职责不仅限于测序；它还负责生成 L2 块、定期向第 1 层提交第 2 层交易和状态更改，以及解决提交的任何潜在挑战。

由于集中式排序器对第 2 层交易的排序和打包具有唯一的控制权，因此带来了挑战。这种垄断引起了人们的担忧，很大程度上源于这种集中控制。


### What are the problems with centralized sequencers?

#### Vulnerability of a Single Point of Failure

第 2 层的正常运行本质上与定序器的操作相关。如果排序器停止工作，来自所有第 2 层用户的交易将不会得到处理，从而有效地降低第 2 层操作。当单个实体控制定序器时，问题会被放大。如果实体发生故障，整个第 2 层就会瘫痪，使系统容易出现单点故障。因此，集中式排序器对 Layer 2 的稳定性构成了重大风险。

#### Excessive Transaction Censorship

集中式排序器有能力拒绝用户提交的交易，使它们无法处理——这是一种公然的交易审查形式。在中心化的第 2 层故意阻止涉及其治理代币的交易的情况下，用户可能会出现恐慌和抛售。
一些解决方案允许用户直接在 Layer 1 上提交他们想要的交易。然而，这个过程非常耗时，通常需要几个小时，并且会给用户带来 Layer 1 的 Gas 费负担。因此，这种替代方案并不能从根本上解决问题。
在去中心化排序器框架中，如果一个排序器拒绝一笔交易，用户仍然可以将其转发给其他排序器。下一个区块的内容最终通过共识确定，确保没有任何一个实体可以根据个人利益审查交易。



#### Monopoly Over MEV

由于排序器可以确定接收到的交易的顺序（或“序列”），因此它实际上垄断了所有矿工可提取价值（MEV）。在这种情况下，用户必须承担排序器对 MEV 的独占控制所带来的任何潜在损失，从而需要对排序器建立额外的、无根据的信任层。
去中心化排序器在多个以 MEV 为目标的实体之间引入了竞争动态。这种竞争消除了任何单一测序仪的垄断，减轻了未经检查的 MEV 对用户的不利影响。



## What's Morph's Approach to Decentralized Sequencers?

Morph 与其他 Rollup 项目不同，因为它从一开始就强调建立去中心化的排序器网络。该设计遵循以下核心原则:

### Efficiency:​
Morph 首先是一个以太坊扩展解决方案，专注于提高效率和降低成本。我们的解决方案必须保证第 2 层的快速执行和交易确认，同时保持尽可能高的去中心化水平。

### Scalable and Manageable:​
定序器网络的设计优先考虑易于维护、扩展和更新。如果一项网络功能需要维护，则不应干扰其他功能的运行。此外，随着新的、更高效的解决方案的出现，测序仪网络应该具有适应性并易于升级。

### Solutions Formulated on These Principles​
基于这些原则，Morph 的排序器网络设计包括：
- 模块化：该结构强调松散连接的模块化组件，允许快速升级或替换。
- 拜占庭容错 (BFT) 共识：排序器采用 BFT 共识来生成 L2 区块。
- 用于批量签名的 BLS 签名：排序器使用 BLS 签名方法对一组 L2 区块进行签名。然后，L1 合约通过 BLS 签名验证此 L2 共识。


:::tip
为何选择 BLS 签名？

目前以太坊中的ECDSA等基础签名算法成本过高。出现这个问题是因为签名数据需要提交给Layer 1合约，并且需要支付相应的费用。随着验证者数量的增加，这个成本也会成比例增加。通过使用BLS签名，上传签名的成本可以保持在恒定水平，不受定序器数量逐渐增长的影响。

:::



### Architecture

下面是Morph去中心化测序网络架构的简单说明。


![Sequencer Network Archi](../../../assets/docs/protocol/dese/seq1.png)


#### Sequencer Set Selection

A complete Morph decentralized sequencer network consists of two parts:

- **Sequencer Set** : This forms the core group that provides sequencing services
- **Sequencer Staking Contract**: This contract facilitates the selection of the sequencer set via an election process. 

通过定序器质押合约，成员被选入定序器集合，共同为 Morph 网络提供服务。选举结果会定期同步到 Layer 1 Rollup 合约。该同步数据用于获取定序器网络参与者的 BLS 聚合签名以进行比较和验证。

### Layer 2 Blocks Generation

鉴于 Morph 的模块化设计，每个定序器都运行一个共识客户端，该客户端运行 BFT 来与其他定序器进行通信。

![Block Generation](../../../assets/docs/protocol/dese/block-con.png)

遵循 BFT 共识协议，选定的定序器从内存池中提取交易，构建区块，并将这些块与其他定序器同步以进行验证和投票。最终结果是生成新的第 2 层块。

### Batching

考虑到在第 1 层上传和验证签名的成本，排序器将在指定检查点用 BLS 签名对一批区块进行签名。

![BlockSign](../../../assets/docs/protocol/dese/batch-sign.png)

签名后，指定的定序器通过其批次提交器组件将集体批次的块转发到第 1 层。

### Consensus Verification

The selected sequencer must submit to the Layer 1 contract:

- 聚合的 BLS 签名
- 交易批次
- 共识确定的状态

Layer 1 合约将验证提交的签名以确认交易的共识。

## Summary 

- Morph 运营一个基于 BFT 共识的原生去中心化测序网络。
- 通过协议和网络优化，Morph在确保去中心化的同时最大化以太坊的可扩展性。
- 基于BLS签名，第一层和第二层的其他参与者可以有效验证第二层的共识结果，确保排序器网络提供的安全性在第一层是可确认的。


## Roadmap

**第一阶段**：在 morph beta 测试网上进行封闭测试

**第二阶段**：去中心化排序器网络在主网上线

**第三阶段**：排序器集合公开选举

**第四阶段**：向公共 l2 空间开放 Morph 的排序器网络
