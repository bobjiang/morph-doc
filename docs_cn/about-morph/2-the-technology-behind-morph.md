---
title: Morph 背后的技术
lang: zh-CN
keywords: [morph,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


## Decentralized Sequencer Network

Morph 的去中心化排序器网络旨在增强区块链的安全性和可靠性。与依赖集中式排序器的传统 2 层解决方案不同，Morph 采用去中心化排序器网络。这种设置确保没有任何一个实体能够控制交易排序过程，从而消除单点故障的风险。如果一个排序器发生故障或恶意行为，其他排序器可以继续处理交易，从而保持系统的完整性和正常运行时间。这种去中心化还可以防止交易审查，并确保没有任何一个实体可以垄断矿工可提取价值（MEV），为所有用户创造一个更公平的环境。

这种协作方法不仅提高了安全性，还提高了事务处理系统的整体效率和可靠性，使 Morph 成为强大且有弹性的 2 层解决方案。


![Sequqencer Network](../../assets/docs/about/overview/seq1.png)

访问 Morph’s[Decentralized Sequencer Network](../how-morph-works/decentralized-sequencers/1-morph-decentralized-sequencer-network.md)以获得更全面的文章。


## Optimistic zkEVM Integration

Optimistic Rollup 和零知识 (ZK) Rollup 是在第 2 层扩展区块链交易的两种不同方法。Optimistic Rollup 只是假设在以太坊上提交批量结算时所有交易都是有效的。然而，任何交易的有效性都可以被称为挑战者的实体通过提交欺诈活动的证据来质疑。如果防欺诈成功，则错误的交易将被拒绝，从而确保安全，但代价是一些潜在的延迟和与挑战过程相关的高额 gas fee。


另一方面，ZK rollups 在提交结算之前使用加密证明来验证交易的有效性。所有批次都有自己的 ZK 证明，允许在主链上快速验证，而无需审查与每笔交易相关的所有数据（因此“零知识”）。这提供了立即确定性和更高的安全性，但生成这些证明需要大量计算且成本高昂。


Morph 的混合 Rollups 结合了这两种方法的优点。最初，系统以 Optimistic 的方式运行，假设交易有效，以便快速处理并降低成本。当交易在 Morph 的挑战窗口内受到质疑时，需要排序器生成 ZK 证明来验证交易。我们将这种方法称为响应式有效性证明 (RVP)。它具有以下改进：

- 效率和速度：典型的 7 天挑战窗口可以缩短到 1-3 天（挑战者不再需要额外的时间来识别恶意提交、创建证明并参与多轮挑战程序）。
- 降低成本：采用 ZK 证明意味着只保留最少的交易信息，从而显着降低 L2 提交的成本。当没有挑战时，可以忽略 ZK 证明提交和验证的成本。因此，RVP 比 Optimistic rollups 和 ZK rollup 更具成本效益。    


![Sequqencer Network](../../assets/docs/about/overview/opzk.png)

访问[Responsive Validity Proof](../how-morph-works/optimistic-zkevm)以获得更全面的文章。

## Modular Design

Morph 的核心是使用复杂的模块化设计架构构建的。该平台分为三个功能模块（Sequencer Network、Rollup、Optimistic zk-EVM），每个模块都由不同的角色定义，这些角色在各种配置中进行协作以满足不同的需求。这些模块中的每个角色都操作其特定的组件，保持功能独立性。这种模块化结构不仅增强了灵活性和适应性，而且增强了系统的可组合性。它实现了高效、互动的生态系统，支持我们平台的各种运营需求。


![Sequqencer Network](../../assets/docs/about/overview/modu.png)



访问[Morph’s Modular Design](../how-morph-works/2-morph-modular-design.md)以获得更全面的文章。