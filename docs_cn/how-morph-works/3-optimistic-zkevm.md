---
title: 乐观zkEVM
lang: zh-CN
keywords: [morph,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


![RVP](../../assets/docs/protocol/resvapro/rvpbanner1.jpg)

## Introduction to State Verification

第 2 层状态验证传统上分为两类：欺诈证明和有效性证明。Morph 引入了一种称为响应有效性证明 (RVP) 的新验证方法，结合了两种方法的优点来解决它们的局限性。欺诈证明虽然有效，但存在资本效率低和安全性假设低的问题。此外，没有一个 Optimistic Rollup (OP-Rollup) 完全实现了无需许可的欺诈证明挑战机制。相反，有效性证明提供了高安全性，但在成本和效率方面面临实际问题，阻碍了 Rollup 的可扩展性。


## The Problem with Optimistic Rollups

在此模型中，第 2 层 (L2) 乐观地假设排序器提交的状态更改是有效的，而无需主动验证其真实性。相反，在第 1 层 (L1) 上确认状态更改之前会引入挑战期。在此期间，外部挑战者根据自己同步的网络状态来验证排序者的提交。如果发现差异，挑战者可以在 L1 上触发挑战过程，以防止错误的状态被确认。

**挑战机制**：虽然所有 Optimistic Rollup 都声称实现了欺诈证明，但只有 Arbitrum 在主网上成功部署了欺诈证明。此外，挑战者通常仅限于几个白名单地址。目前 Optimistic Rollup 项目中的欺诈证明可以分为两类：

**非交互式欺诈证明**：当对排序器提交的新状态进行挑战时，L1 会重新执行所有相应的 L2 交易，以生成有效状态，以便与排序器提交的状态进行比较。这个过程会产生大量的 gas 成本，并且可能导致 L2 和 L1 之间的差异，因为某些交易在 L2 上产生的结果可能与 L1 不同，或者 L1 可能无法执行某些 L2 交易。Optimism（OP）曾经使用过这种方法，但由于这些问题而放弃了它。

**交互式欺诈证明**：为了解决非交互式欺诈证明的问题，引入了多轮交互式欺诈证明。该方法通过定序者和挑战者之间的多轮交互来确定导致错误的具体指令执行，然后通过在L1上执行相应指令来确认欺诈。这种方法降低了计算成本并减少了 L1 和 L2 之间结果不一致的问题。然而，它引入了复杂性，例如： - 实施难度较高 - 更长的挑战周期（必须为复杂的互动作业足够的时间） - 提高标准，影响挑战者的积极性

目前，Optimistic Rollup 项目中只有几个 OP Rollups 在其主网上实现了完整的交互式欺诈证明机制。相比之下，多个 ZK-rollup 项目已经在主网上启动。

这些复杂性凸显了改进现有乐观汇总模型的必要性。因此，Morph 引入了响应有效性证明（RVP）。




## What is RVP?​

![RVP](../../assets/docs/protocol/resvapro/compare3.png)

Responsive Validity Proof (RVP) integrates ZK-based validity proofs into the optimistic rollup framework. The process is as follows:

当挑战者检测到定序器提交了错误的数据时，他们会向第 1 层 (L1) 上的定序器发起挑战请求。然后，定序器必须在指定时间（挑战期）内生成相应的零知识（ZK）证明并通过 L1 合约的验证。如果验证通过，则挑战失败；否则，挑战成功。此过程结合了乐观汇总和 ZK 汇总的优点，提供了安全性和效率的平衡方法。

### Advantages of RVP Compared to Interactive Fraud Proofs

1. **缩短挑战期**：RVP 可以将挑战期从通常的 7 天缩短到仅 1-3 天，从而提高整体效率和用户体验。
2. **降低 L2 提交成本**：通过使用有效性证明，第 2 层 (L2) 不需要包含大多数交易字节，从而显著降低提交成本。
3. **改善挑战者体验**：使用 RVP，挑战者只需发起挑战。排序器必须通过生成和验证相应的 ZK 证明来证明其正确性，从而简化挑战者的职责。
4. **无缝过渡到 ZK-Rollup**：RVP 的架构设计允许轻松过渡到完整的 ZK-rollup。所需的主要更改是将排序器的 ZK 证明提交方法从响应式调整为主动式。

RVP 通过结合 ZK 证明来增强乐观汇总模型，提供更高效、更具成本效益且安全的解决方案。它解决了传统欺诈证明的局限性，并为未来无缝过渡到完整的 ZK-rollup 实施铺平了道路。

### How Can RVP Shorten the Challenge Period of an Optimistic Rollup?	
#### The Need for a Challenge Period
乐观汇总包含挑战期（或退出期），以确保排序器的任何恶意提交都可以被识别和质疑。这段时间为挑战者提供了足够的时间来验证交易、进行欺诈证明并完成挑战过程，从而确保在第 1 层 (L1) 上仅确认有效的状态更改。
两个主要因素影响挑战期的长度：
1. 完成时间：双方完成挑战过程所需的时间。
2. 减轻恶意行为：确保有足够的时间来应对排序器在 L1 上恶意阻止挑战者交易的任何企图。

#### Solutions to Shorten the Challenge Period
**简洁直接的挑战Process:**对于多轮交互式欺诈证明，整个挑战过程可能需要多轮交互，每轮都需要大量时间。例如，如果该过程需要 10 轮，则考虑到来回响应，至少需要 20 个时间块才能完成挑战。
相比之下，RVP 简化了挑战过程，只需要一次交互：排序器上传批次的 ZK 证明，然后在 L1 上进行验证。这个简化的流程解决了挑战者是否有足够的时间检测和证明错误的主要问题，从而大大缩短了挑战时间。

**Protection Against Malicious Behavior**: 在交互式防欺诈系统中，被挑战方可能会试图干扰挑战进程，比如对 L1 发起 DoS 攻击，以阻止挑战者与 L1 交互并提交证明。
通过RVP，挑战者只需触发挑战即可。一旦发起挑战，定序器就没有机会干预。然后，定序器必须通过 ZK 证明证明其提交的正确性。这保证了正常的挑战过程不会受到恶意行为的影响，进一步缩短了挑战周期。

#### Key Benefits of RVP in Reducing the Challenge Period
- **效率**：RVP 所需的单次交互简化了挑战流程，减少了解决所需的时间。
- **安全性**：通过依赖 ZK 证明，RVP 提供了一种强大的机制来验证状态变化，而无需冗长的交互。
- **成本效益**：交互次数的减少降低了与 L1 上的挑战流程相关的 gas 成本。

通过解决这些因素，RVP有效地将挑战周期从传统的7天缩短到仅需1-3天，为Optimistic Rollup提供了更高效、更安全的解决方案。

### Why is the Operating Cost Lower for L2 Based on RVP?	

#### Compression of Transactions

在 ZK-rollups 中，每笔交易的有效性都是通过提交的 ZK-proof 来确认的，这样就不需要包含大量的交易细节。例如，以太坊交易的长度约为110字节，签名约占68字节。在乐观汇总中，由于交易需要在 L1 上重放，因此必须包含这些签名以确保有效性。这增加了成本。
然而，ZK-rollups 只需要保留基本的交易信息，因为有效性证明涵盖了整个批次。这种压缩功能减少了需要提交到 L1 的数据量，从而显着降低了成本。

#### Efficient Data Submission

RVP利用ZK-proofs来验证交易，在批量数据提交过程中采用ZK-rollup的交易压缩优势。这减少了总体数据量和相关成本。此外，当没有挑战时，排序器不会产生生成和提交 ZK 证明的成本，从而进一步降低运营费用。

#### Comparison with Existing Solutions

The design of RVP ensures that the cost of rollup operations is lower than that of both existing optimistic rollups and traditional ZK-rollups. This efficiency is achieved by:
- 减少 L1 上详细交易重放的需要。
- 仅在必要时利用 ZK 证明，最大限度地减少不必要的证明生成成本。

### RVP is Friendly to Challengers
The core of RVP is the use of validity proofs to ultimately validate challenged data. This benefits challengers in the following ways:
1. **简化的挑战Process:**
- 在RVP中，定序器负责生成和验证证明。挑战者只需通过质押发起挑战，降低挑战者的复杂度和负担。
- 这与传统的欺诈证明形成鲜明对比，在传统的欺诈证明中，挑战者必须与排序器多次交互，使得过程繁琐且复杂。
2. **Lower Threshold for Challengers**:
- 在许多 Layer 2 项目中，由于潜在的高回报，测序者有很高的动机进行恶意行为。相反，挑战者通常看到的直接利益较低，导致缺乏挑战欺诈交易的动力。
- RVP 通过将证明生成的责任转移给排序器来降低挑战者的门槛，从而增加检测和纠正欺诈行为的可能性。
3. **Mitigating Malicious Challenges**:
- 虽然挑战者存在发起不必要的挑战以增加测序者成本的风险，但 RVP 通过要求挑战者补偿测序者在挑战不成功时产生的成本来减轻这种风险。
- 该机制阻止无意义的挑战并确保仅提出合法的争议。

通过采用这些策略，RVP 确保了验证第 2 层交易的更公平、更高效的流程，最终降低运营成本并增强网络的安全性和完整性。

### Why do sequencers have to take on the responsibility of submitting ZK-proofs?​

一些提案建议挑战者可以通过提供自己的提交和相应的 ZK 证明来证明排序器提交的虚假性。然后可以比较这两个提交，以识别排序器是否存在欺诈行为。然而，这种方法存在很大的问题:

挑战者需要使用排序器提供的交易生成 ZK 证明。如果排序器提交无效交易，则挑战者无法创建可在第 1 层 (L1) 上进行身份验证的 ZK 证明。因此，测序者证明其提交的正确性更为有效。这种方法确保负责交易的实体验证其准确性，维护系统的完整性。
### Why Not Simply Employ ZK-Rollups?

虽然像目前的 ZK-rollups 一样，通过大量加密计算来验证排序器每次状态提交的有效性，理论上可以提供更高的安全性，但这种方法也带来了一些挑战:

#### The Cost of ZK-Rollup

目前，zkSync、Polygon zkEVM等项目已在主网上线，这表明生成和验证ZK-proofs不再是最紧迫的问题。然而，这些 ZK 证明仍然面临成本和效率的限制。例如，zkSync Era 的平均交易成本从 0.51 美元到高达 310 美元不等，具体取决于 L1 汽油费。这比 Arbitrum 和 Optimism 等 Optimistic Rollup 项目的交易成本要昂贵得多。相比之下，使用 RVP，通过仅在受到挑战时使用 ZK 证明来压缩交易数据，可以避免正常网络运行期间的高成本。正常运营所需的成本最低，保持效率和可承受性。

#### Block Finalization Time in ZK-Rollups

理论上，ZK-rollups 应该没有退出期，因为通过 ZK-proof 的整个 L2 状态转换验证过程应该在几分钟甚至几秒内完成。然而，实际情况却有所不同。由于技术限制，L1 上 ZK-proofs 最终验证所需的时间比预期慢得多。例如，zkSync Era L2 区块最终确定大约需要 20-24 小时，这与 Optimistic Rollup 的优化提现周期没有显着差异。

#### Seamless Transition with RVP-Based Rollups

结合 RVP 技术的 L2 扩展解决方案可以使用 ZK-rollup 框架进行设计，随着 ZK 技术的成熟，可以轻松地从基于 RVP 的 L2 过渡到标准 ZK-rollup L2。所需的主要调整是将定序器的 ZK 证明提交方法从响应式更改为主动式。因此，基于 RVP 的系统将来可以无缝地采用 ZK-rollup 的全部优势。
