---
title: Morph的架构
lang: zh-CN
keywords: [morph,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


:::tip

本概述简要介绍了 Morph 的汇总技术堆栈。如需深入了解，请参阅我们文档的“Morph 工作原理”部分。

:::


![Archi](../../assets/docs/about/architecture/archi.png)


## The Modular Approach in Layer 2

传统上，模块化的概念已应用于第 1 层区块链，将它们划分为不同的层。在 Morph，我们已将这种模块化理念扩展到第 2 层，并围绕这一原则构建我们的平台。

在典型的第 1 层区块链中，架构由四个主要层组成：
- 共识：实现网络协议的机制。
- 执行：交易处理和智能合约操作发生的地方。
- 结算：完成交易的过程。
- 数据可用性：确保可以访问必要的信息进行验证。

在第 2 层的背景下，Morph 以独特的功能重新诠释了这些层：

- **通过去中心化排序器网络达成共识和执行**：在 Morph，这些功能由我们的去中心化排序器网络集成和处理。排序器协调、处理并达成第 2 层交易的共识，形成用户交互的主要界面。


![Archi](../../assets/docs/about/overview/seq1.png)

- **使用 Optimistic zkEVM 进行结算**：Morph 中的结算是指在以太坊层面完成第 2 层交易。它涉及验证第 2 层状态的关键步骤。Morph 为此采用了 Optimistic zkEVM，这是一种融合了Optimistic rollups和 zk-rollups 优点的混合方法。第 2 层状态最终将在明显更短的挑战期内完成，或者如果受到挑战，则通过相应的 zk-proof 完成。

![Archi](../../assets/docs/about/overview/opzk.png)

- **通过“Rollup”流程实现数据可用性**：这需要将重要的第 2 层数据传输到以太坊。在 Morph 中，这是通过“Rollup”流程实现的，其中批量提交者将区块编译成批次并将它们作为第 1 层交易提交到以太坊上。


![Archi](../../assets/docs/about/architecture/rollup.png)

## 独立但协作的功能
这些主要功能中的每一个都独立运行，促进异步任务和可切换的实现：

1. Sequencer Network：执行第 2 层交易并更新本地状态。
2. Rollup Module：将第 2 层块转换为批次以提交给第 1 层。
3. 状态验证：利用第 1 层安全性在 Optimistic 的 zkEVM 规则下验证第 2 层状态。


这种模块化架构增强了 Morph 生态系统内的灵活性、适应性和可组合性。


## Diverse Roles

Morph 的架构进一步由五个关键角色定义：排序器、验证器、节点、证明器和第 1 层（以太坊）。每个角色都承担特定的职责，并利用不同的组件来实现其功能，从而促进网络的无缝运行。

要更深入地了解 Morph 的架构，请访问我们的综合[Developer Docs](../build-on-morph/0-developer-navigation-page.md).

