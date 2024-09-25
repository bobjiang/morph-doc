---
title: rollup
lang: zh-CN
keywords: [morph,ethereum,rollup]
description: 解释 Morph 中汇总过程的工作原理
---


:::info

作为 Layer 2 项目的基础，“Rollup”过程是指 Layer 2 将 L2 交易和状态组装成批次，然后将其与 L2 状态一起提交到 L1 的方法。

之内[Morph's architecture](../2-morph-modular-design.md)，这个 Rollup 过程是由```Batch Submitter```成分。

:::

### An overview of Morph Rollup Design:

![rollup](../../../assets/docs/protocol/general/rollup/rollup.png)


## Constructing the Batch​

定序器内的 L2 节点根据共识结果生成 L2 区块并更新 L2 的本地状态。批次提交者必须查询 L2 节点以检索最新的 L2 块。

然后，批处理提交者重建 L2 区块，编译：

- 交易：区块中包含的所有交易。
- 区块信息：每个区块的基本信息。

批处理提交者继续获取和重建区块，直到它处理带有 BLS 签名的区块，表明已达到批处理点。重建的区块数据用于构建批处理，其中包含：

- lastBlocknumber：批处理中最后一个区块的编号。
- 交易：批处理内的编码交易。
- BlockWitness：编码的区块信息，用于 zkProof。
- PreStateRoot：批处理应用之前的 stateRoot。
- PostStateRoot：批处理应用后的 stateRoot。
- WithdrawalRoot：L2 提款 Merkle 树根。
- 签名：批处理的 BLS 签名。


:::info

Morph采用zk技术​​来证明提交的批量数据的准确性，所以需要Blockinfo（BlockWitness）。它充当零知识证明中的见证人。

:::


## Putting Multiple Batches into a Single Rollup Transaction​


虽然汇总项目的标准是每个 L1 汇总事务仅包含一个批次，但 Morph 通过将尽可能多的批次插入到单个 L1 事务中来进行优化。
这种效率驱动的方法显着降低了总体成本，因为 L1 费用是与 L2 相关的交易成本的主要组成部分。通过优化可用空间的利用，Morph 在不影响交易完整性的情况下实现了成本效益。




## Submitting Batch Data to the Rollup Contract​

批次提交者最终将把以太坊交易从其 L1 账户发送到 Morph 的主合约。

交易的calldata包含批次数据。

:::info

根据ERC-4337的开发流程，未来批量数据可能会被纳入新的“blob”结构中，以进一步降低成本。

:::

一旦交易在以太坊上提交并确认，验证器节点就可以使用批次内的交易数据重建并验证排序器提交的有效性。


## Finalize the batches

根据 Morph 的规定，批次是否有效[responsive validity proof](../3-optimistic-zkevm.md)标准下，批次内的所有交易都将被最终确定，包括提现交易。

这样，提现请求就会得到满足，相应的第一层锁定资产就会被释放。


# Decentralize Batch Submitter


## What is Batch Submitter?



A Batch Submitter plays a crucial role in the "rollup" process, acting as the bridge that connects Layer 2 (L2) data with Ethereum (Layer 1 or L1). Their primary responsibilities include:
- 收集 L2 交易和块数据，将它们组装成一个有凝聚力的批次。
- 将此批次数据嵌入到第 1 层事务中。
- 通过调用Layer 1合约来执行此交易，完成rollup过程。


![rollup](../../../assets/docs/protocol/general/rollup/rollup.png)

## What is the relationship between Sequencers & Batch Submitters？

批处理提交者功能通常集成在更广泛的“排序器”角色中。在分散式定序器网络架构中，每个定序器都配备或可以访问批次提交器组件。这种整合是实现和维持最高水平的去中心化的关键。

这种结构确保上传到第 1 层的数据保持分散，防止单个实体控制汇总过程。

## How to decentralize the Batch Submitter？

为了坚持上述原则，必须确保多个序列器能够在同一时间范围内均匀地分担汇总任务。我们实现此目标的方法涉及一个轮换系统，让序列器轮流负责调用批处理提交者，如下所述：

### 提交者轮换

- **Epoch 周期角色切换**：序列器在既定的 Epoch 周期内交替担任批处理提交者。
- **跨 Epoch 执行能力**：任何序列器都可以为另一个序列器的 Epoch 执行汇总。
- **超时日志记录**：系统记录在某个 Epoch 期间没有发生单个汇总的情况，该 Epoch 以及负责的序列器将被标记为“超时”。

### 超时

- **超时标识**：如果某个 Epoch 过去而没有汇总（批处理提交），则将其标识为“超时”。 Rollup 的时间与第 1 层 Rollup 交易的确认时间挂钩。

- **Epoch 轮换**：一个 Epoch 的持续时间和轮换计划由序列器网络治理决定。序列器被分配索引，这些索引决定了它们对一个 Epoch 的责任。随着序列器集的变化，索引会被重新分配，并且 Epoch 会根据这些新分配相应地轮换。

### 超时惩罚
- **累积惩罚**：经常表现出超时行为的序列器可能会面临与其第 1 层 ETH 质押相关的惩罚，如果超时记录达到一定水平，序列器可能会/将被从序列器网络中削减。

## 模块设计 下面你可以找到负责各个模块的合约及其职责： ### Layer1 - **RollupContract**：记录 Rollup 执行器并与 L2 同步 ### Layer2 - **SequencerContract**：同步序列器 - **GovContract**：管理 Batch & Epoch 参数 - **SubmitterContract**: - 记录纪元信息 - 记录汇总历史 - 记录提交者工作量 - 记录提交者超时 - **IncentiveContract**:采取激励和惩罚措施

