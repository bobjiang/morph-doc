---
title: Morph 的 Stake 系统设计
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


# What is Morph Staking System?

:::tip
目前Stake系统正处于Beta测试阶段，本文档中描述的设计会随着测试过程的进行而发生变化，并不代表主网的最终体验。
:::

Morph Stake是一个建立在去中心化排序器网络之上的完整的经济和工程系统，以确保网络的运行和安全。

It can be divided into 2 parts:

**ETH质押**

在以太坊上，潜在的排序者需要在第 1 层质押合约中质押 ETH，才能首先成为质押者。

ETH 质押会增加测序者恶意行为的成本。

如果测序者确认存在不诚实或疏忽，质押的 ETH 将被削减。所需的 ETH 质押金额是不可变的。

**Morph 代币质押**

Morph token 是 Morph 的治理代币（Gas token 是 ETH）。在 Staking 系统中，它将扮演以下角色: 

根据代币持有者委托给他们的 Morph 代币数量，Staker 被选为排序者。因此，质押者需要吸引 Morph 代币持有者将代币委托给他们。只有排序者才能获得网络奖励。
Morph 代币持有者可以将其代币委托给任何质押者，这将决定是否可以选择质押者作为排序者。排序者根据排序者的贡献从 Morph 代币的通货膨胀中获得奖励，委托者根据委托金额分享一部分奖励。

## Roles within the Staking System:

1. Staker（排序器候选人）：任何人（前期需要在白名单中）都可以将 ETH 质押到 L1 质押合约中并成为质押者。只有质押者可以参加排序器选举。
2. 排序器：排序器能够执行排序器任务并从中获得奖励。排序器是根据 Morph 代币的委托量来选择的。
3. 委托人：Morph 代币持有者可以将其代币委托给任何质押者。委托人可以根据委托量分享委托排序器获得的奖励。

## Details of sequencer set election:

The determination of the sequencer set will be based on two points:

1. 测序者必须在第 1 层质押合约中质押固定数量的 ETH。
2. 假设排序器集合的最大大小为X，根据Morph代币的委托数量，从所有有效候选者中选择最多X个排序器作为排序器集合。


排序器集合将根据上述原理进行实时更新。

当有新的 MorphToken 质押时，L2 质押合约将检查这是否会导致排序器集发生更改，并在需要时更新排序器集。

加入排序器集合意味着所有排序器将有权利参与当前的网络运行以获得奖励，同时也承担维护网络高效正常运行的责任。

实际上，每个排序器，无论委托数量如何，都具有相同的权重。

排序器可以随时退出。他们需要提交第一层质押合约的退出请求，然后进入锁定期。当 Layer 2 合约完成退出过程并达到解锁区块高度后，它们将被解锁并可以领取质押的 ETH。


## Rewards & Slash

### Rewards

Morph 生态系统内的测序者有 3 种潜在奖励。

**L2 MorphToken 质押奖励。**

Morph 代币具有通胀性，每年会增加初始最大总供应量的 6%，作为 L2 Morph 代币质押奖励。

这 6% 将每天（一天为一个纪元）分发给所有当前正在运行的排序器。

排序者将先收取佣金，然后根据委托人的委托金额将剩余部分分配给委托人。

**L2 气体Income:**

排序器从第 2 层用户处获取 ETH（第 2 层收入），并花费 ETH 将批次提交到第 1 层（第 1 层成本）。

如果Layer1成本小于Layer2收入，则剩余价值理论上就成为Layer2的利润。

一开始，网络收集所有 Layer2 收入，并向排序器支付 ETH 以支付其 Layer 1 成本。未来我们会对这部分资金的使用有更详细的计划。

**ETH重新质押yield:**

为了提高资金效率，我们计划利用staker的ETH押金在重质押产品中产生收益，收益仍会分配给staker。



#### How to decide each sequencer’s MorphToken rewards?

这是基于区块生产记录。

In each epoch, the total reward received by each sequencer and their delegators is calculated as follows:

**sequencer_reward = (sequencer_ Produced_block / Total_ Produced_blocks) * Total_morph_token_inflation **


排序器奖励最终分配给委托人（尽管排序器也可以是自己的委托人）。 Sequencer可以设置佣金比例从中抽取分成，并且比例可调。

**sequencer_commission =equencer_reward *commission_rate**


The reward each delegator of this sequencer receives is the remaining portion multiplied by the percentage of their staked amount:

**delegator_reward = (sequencer_reward -equencer_commission) *delegation_amount /total_delegation_amount**

用户的委托奖励将从用户质押后的下一个周期开始计算。

**Example:**

如果今天（这个纪元）的总 Morph Inflation 是 100，并且这个纪元产生了 100 个区块。

Sequencer A produced 10 blocks within this epoch, so he will receive:

**sequencer_reward = (sequencer_ Produced_block / Total_ Produced_blocks) * Total_morph_token_inflation = (10/100) * 100 = 10 MorphToken。**

如果排序者的佣金率为5%

**sequencer_commission =equencer_reward *commission_rate = 10 * 0.05 = 5 MorphToken**

如果一位委托人质押了 100 个 MorphToken，则总共有 1000 个 MorphToken 委托给了排序器。

**delegator_reward = (sequencer_reward -equencer_commission) *delegation_amount /total_delegation_amount = (100 - 5) * (100/1000) = 9.5 MorphToken**

理想情况下，由于每个排序器的权重相同，因此每个排序器将能够在特定时期内产生相同数量的块。因此他们的奖励应该是相同的。

然而，如果排序者未能履行其职责，区块产量将大大降低，因此他们的奖励也会低得多。


### Slash

基于乐观的 zkEVM 设计，将会有验证者不断验证排序者提交的批次，如果他们认为排序者存在欺诈行为，验证者将通过 L1 rollup 合约发起挑战。

[Read more about the challenge here:](../3-optimistic-zkevm.md)

To prevent fraudulent behavior by Sequencers from affecting network security, the following rules need are established:

- 验证者将挑战固定批次，所有签署该批次的测序者将集体受到挑战。
- 当排序器承担批次提交者的角色时，重复超时累积到一定程度将导致奖励被扣除或从排序器集合中移除（尚未完全实现）。
- 长期未产生区块的排序器将从排序器集中删除（尚未完全实现）。

:::tip
提交者轮换和提交超时是去中心化 Rollup 设计的一部分，您可以阅读详细信息[here](../general-protocol-design/1-rollup.md).
:::

For the reward and slash functionalities, we have 2 contracts:

- L2 Record Contract: The off-chain data affecting rewards and penalties will be collected and recorded in the L2 Record contract through an Oracle, primarily consisting of rollup data and Block data.
- L2 Distribute Contract: Sequencers and Delegator will manually claim rewards based on the Record.

## Governance:

我们现在有一个治理合约来决定一些网络参数。目前，只有排序者可以创建提案并投票。

在路线图的下一阶段，我们计划建立一个完整的治理系统，允许所有 Morph 代币持有者决定网络的各个方面。

## Major Process

### Staking & Sequencer Selection

Morph token staking will be divided into 2 stages based on the network status:

- Phase 1: Morph token inflation and staking rewards not started yet.
序列器选举一开始将是 FCFS，但允许委托权益。由于还没有新的代币生成，因此没有变形代币奖励。

- Phase 2: Morph token inflation and staking rewards is started.
排序者选举将正式开始，根据Morph代币的委托数量，奖励也将开始分配。

排序器集是如何生成的？

1.`L1` Staking Contract: 将潜在的sequencer添加到白名单。
2.`L1` Staking Contract: 潜在的sequencer将能够在以太坊上注册并质押eth，从而有资格参加sequencer选举（成为staker）。
3.将`add straker`消息作为跨层消息从 L1 质押合约发送到 L2 质押合约。
4.`L2` Staking Contract: 将使用同步的消息更新staker。
5.`L2` Staking Contract: 用户将能够将MorphToken委托/取消委托给staker。
6.`L2` Sequencer Contract: L2 Staking Contract将通过调用L2序列器联系人根据Morph token委托量的排名来更新sequencer集合，排名最高的staker将被选为sequencer。

### Sequencer network consensus & Verification on Layer 1

- 每个提交的批次都需要排序器集中超过 2/3 的排序器的 BLS 签名才能被 L1 rollup 合约接受。

Notice: Currently, the BLS 12-381 signature pre-compiled contract has not been implemented on Ethereum. Therefore, the L1 rollup contract cannot verify whether the batch is signed by the L2 sequencer set.
在此功能可用之前，汇总合约仅允许白名单中包含的涉众批量提交。这项措施的实施是为了让我们能够在出现欺诈性提交的情况下大幅削减 ETH 押金。实施签名验证后，提交者将成为无权限的，签署欺诈批次的测序者将代替提交者被削减。


1.`L1` Rollup Contract：批次提交者将批次提交给 Rollup Contract。
2.`L1` Rollup Contract：Rollup Contract 验证批次的 BLS 签名，并将其与来自 L1 质押合约的序列集同步进行比较。只有验证通过，它才会接受批次。

### Slash for Sequencers

#### What happens if validators successfully challenge sequencers?

- 如果挑战者成功，排序器将被削减所有质押的 ETH 并从排序器集中删除。
- 即使通过多次挑战证明存在欺诈行为，每个排序器也只会被削减一次。
- 挑战成功的挑战者奖励为质押金额的固定比例。
- 如果斜杠使所有排序器都停止运行，则 L2 将停止运行。我们可以通过升级 L1 质押合约、重置质押者和排序器集来重新启动。这不会影响第 2 层状态，因为不会因此处理任何事务。

Process:

1.`L1` Staking Contract: Slash staked ETH of sequencers who signed the fraud batch and remove them from sequencer set.
2.`L1` Staking Contract: Distribute validator rewards.
3.A`remove staker`消息将作为跨层消息从 L1 质押合约发送到 L2 质押合约。
4.`L2`Staking Contract: Update sequencer set.

### Delegation Stake

1.`L2` Staking Contract: Staker set delegation commission rate by their own will.
2.`L2` Oracle: Upload sequencers work records (block production records, submitter work records, expect work records) on the epoch basis (an epoch is a day).
3.`L2` MorphToken Contract: Mint MorphToken (inflation) as delegation reward and sent to L2 distributor contract.
4.`L2` Staking Contract: Users claim delegation reward, sequencers claim commission.

### Staker/Sequencer exit

退出锁定期应该足够长，以确保 L2 中的抵押者和排序者已更新，并且大于排序者最后生成的块的挑战期（如果抵押者也是排序者）。


1.`L1` Staking Contract: Stakers apply to exit, the stake ETH is locked to enter the lock period.
2.A`remove staker`消息将作为跨层消息从 L1 质押合约发送到 L2 质押合约。
3.`L2` Staking Contract: Received the message, remove staker, and sequencers (if the staker is also sequencer).
4.`L1` Staking Contract: Withdraw allowed until reach unlock block height，remove staker info after claiming.