---
title: Morph与以太坊之间的通信
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


尽管 Morph 是建立在以太坊之上的 Layer 2 解决方案，但它仍然是一个独立且独特的区块链。因此，在 Morph 和以太坊之间建立通信渠道以促进资产和消息的顺利转移至关重要。通信可以双向进行：从以太坊到 Morph，从 Morph 到以太坊。

## Morph 基础知识 - 以太坊桥​

在以太坊和 Morph 之间转移资产涉及以下过程：

- 资产锁定和包装：要启动转移，用户必须在跨层桥上锁定其资产。锁定确认后，Morph 会铸造一个代表锁定资产价值的包装代币，这个过程称为“存款”。

- 资产接收：铸造后，用户或预期接收者将在 Morph 上收到资产，反映最初锁定资产的价值。

- 逆向过程：相反，要将资产转回以太坊，桥可以通过在 Morph 上销毁包装代币来解锁以太坊上的原始资产。这被称为“撤回”。

此外，这座桥的用途不仅仅限于资产转移。它采用相同的消息传输基本原理，从而能够跨两个网络层传输数据有效负载。


## Understanding the Gateway


网关作为用户与整个网桥系统交互的主要入口点。虽然跨层资产转移的核心流程仍然依赖于消息传输，但我们建议使用 Gateway 方式来实现高效的跨层交易。

针对不同的跨层资产转移需求，我们设计了不同的网关，如ETH网关、标准ERC20网关等。

此外，我们还实现了网关路由器，以根据您拥有的资产类型调用不同的网关。这有利于与网关路由器合约的无缝交互。





| L1 网关合约 |描述 |
| ------------------------ | ---------------------------------------------------------------- |
|`L1GatewayRouter`|网关路由器支持ETH和ERC20代币的充值。 |
|`L1ETHGateway`|存入 ETH 的网关。                                      |
|`L1StandardERC20Gateway`|标准 ERC20 代币存款的网关。                   |
|`L1CustomERC20Gateway`|自定义 ERC20 代币存款的网关。                     |
|`L1WETHGateway`|打包 ETH 存款的网关。                            |


| L2 网关合约 |描述 |
| ------------------------ | ---------------------------------------------------------------- |
|`L2GatewayRouter`|网关路由器支持ETH和ERC20代币的提现。 |
|`L2ETHGateway`|提取 ETH 的网关。                                      |
|`L2StandardERC20Gateway`|标准 ERC20 代币提现的网关。                   |
|`L2CustomERC20Gateway`|自定义 ERC20 代币提现的网关。                     |
|`L2WETHGateway`| Wrapped ETH 提现网关。                            |


## Deposit (L1 to L2 message) 

![Deposit Process](../../../assets/docs/protocol/general/bridge/deposit.png)

### Constructing a Deposit Request Through the Gateway

桥接请求，无论是针对 ETH、ERC20 还是 ERC721，本质上都是跨层消息，需要初始构建消息。

一般来说，消息结构保持一致，特别是对于 ETH 和 ERC20 网关。

使用令牌网关编译标准令牌网关消息并将其中继到```CrossDomainMessenger```.

### Passing the Message Through the CrossDomainMessenger


这```CrossDomainMessenger```作为跨层通信的核心单元，
在第 1 层和第 2 层上都有相应的信使合约。

对于存款，L1 信使会向 L2 信使发送一条消息，类似于第 1 层上的合约调用，这意味着可以构建自定义消息（合约交互）来执行各种类型的跨层交互。

### Executing the Message on Layer 2

跨域消息传递到```L1MessageQueueWithGasPriceOracle```，然后触发一个名为的事件```QueueTransaction```.

排序器将监视此事件并在其下一个块中包含第 2 层事务。


### How to make sure Sequencer doesn't fake a deposit transaction?

排序者可能有动机伪造不存在的存款交易，例如铸造大量第 2 层代币并将其转移到他们拥有的地址。

Morph prevents these risks with two measures:

由于 Morph 的去中心化序列器架构，锻造交易需要控制至少三分之二的序列器，这是一项具有挑战性的壮举。

Morph 乐观的 zkEVM 框架允许挑战者检测此类恶意行为并发起挑战以纠正不当行为。


持有跨层消息的第 2 层执行器与 L2 信使交互以执行消息，其中可能包括将 L2 ETH 或 ERC20 代币转移给接收者。


### Finalizing the Deposit Message

存款过程的完成不仅仅涉及在第 2 层上执行请求。由于通过质询过程识别出不正确的批次数据，因此第 2 层执行及其相应的状态更新可能会被恢复。

因此，只有相应批次的存款执行交易完成后，存款请求才被视为完成。

Typically, this follows a simple workflow:

- 充值执行交易被编译成批次并由批次提交者提交到第1层。

- 挑战期结束后，有效批次将通过后续批次提交最终确定```rollup.commitBatch```.

- 在最终确定期间，```L1MessageQueueAndGasPriceOracle```从队列中移除（pop）存款消息，标志着存款过程完成。



## Withdraw (L2 -> L1 message) 

![Withdraw Process](../../../assets/docs/protocol/general/bridge/withdraw.png)

### Finalizing a Withdrawal

Unlike Deposits, a withdrawal request must undergo 2 processes for execution:

1. 通过根据排序器提交的提款树根验证 Merkle 树证明，证明提款请求确实发生在第 2 层。

2. 等待挑战期结束并最终确定提现树根，解决排序器提交错误批次数据（包括提现树根）的风险。

通常，这两个过程同时发生。一旦提现树根最终确定，用户可以调用```proveAndRelayMessage```内的方法```L1CrossDomainMessenger```合约执行提款消息。

```solidity
function proveAndRelayMessage(
        address _from,
        address _to,
        uint256 _value,
        uint256 _nonce,
        bytes memory _message,
        bytes32[32] calldata _withdrawalProof,
        bytes32 _withdrawalRoot
    )

```

This function serves two primary purposes:

1. 检查与此消息关联的提现树根是否已通过汇总合约最终确定。
2. 通过验证提供的 Merkle 证明来验证提款请求是否实际发生。

成功完成这两个过程后，该方法将执行相应的操作，例如在第 1 层释放用户的 ETH 以进行标准的 ETH 提现请求。


### Understanding the Withdraw Tree

提款操作涉及由于第 2 层交易而与第 1 层资产/合约进行交互。因此，必须以可在第 1 层验证的方式验证触发提款请求的第 2 层交易是否存在。

为了实现这一目标，我们引入了一种称为提款树的结构，它在 Merkle 树中记录每笔 L2 提款交易。因此，可以利用 Merkle 树的属性来确认提款请求的发生。

术语“提现树”是指仅附加的稀疏默克尔树（SMT），其叶节点捕获从网络中转移的资产的信息。
Each leaf in the Withdraw Tree, known as a Withdraw leaf, falls into two categories: type 0 for recording asset(s) information and type 1 for recording messaging information.

特别是，撤回叶子是具有跨域消息的 ABI 编码打包结构的 Keccak256 哈希。

提款树有助于对提款交易进行分类并确定提款请求的合法性。

Morph 预先部署了一个 Simple Merkle Tree 合约，专门用于构建 Layer 2 提现树。

This tree incorporates three methods:

1.```getTreeroot```- 检索当前树的根哈希。
2.```appendMessageHash```- 将新的叶节点追加到树中。
3.```verifyMerkleProof```- 验证树中是否存在叶节点，表明它所代表的桥接请求的有效性。

### Understanding the Challenge Period & Batch Finalization

乐观的 zkEVM 架构要求每个 L2 交易都必须提交到第 1 层，并在最终确定之前经历一个挑战期。

此过程对于验证第 2 层状态至关重要，最终验证提款请求的真实性。

一旦挑战期、批次和状态最终确定，排序器也会提交提款树根，这是提款请求验证的组成部分。

## Cross-layer (Bridge) Errors

通过跨层桥的设计，需要执行存款的跨层消息并更新其第 2 层状态。成功发送跨链请求并不能保证其在L2上成功执行。

在此之前，跨层消息在第2层执行过程中存在失败的可能性。
本节概述了处理失败的跨层存款消息的潜在场景和解决方案。

### Cross-layer (Bridge) Failure Scenarios:
跨层（桥接）通信中可能发生两种主要类型的故障：

1. Gas 故障：由于 gasLimit 或代码逻辑的限制，从 L1 发送到 L2 的跨层消息在 L2 上执行时可能会失败。

2. 跳过消息：某些数据执行可能会触发 L2 节点电路中的溢出，从而导致跨层消息被遗漏或跳过。 

### Handling Cross-layer (Bridge) Failures:

For Gas Failures:

- 当```L1CrossDomainMessenger```L1上的合约发送跨层消息，它记录了相应的消息哈希，但不将gasLimit包含在该记录中。在 L2 上执行后，```L2CrossDomainMessenger```执行等效计算，将合约调用结果存储在```mapping(isL1MessageExecuted)```。该措施可以防止同一消息的多次执行，并有助于调整gasLimit参数以重放失败的消息。

- Replay Message: If gasLimit is insufficient, causing a failed execution on the L2, a new cross-layer message with a revised gasLimit parameter can be sent by calling ```L1CrossDomainMessenger.replayMessage```.

For Skipped Messages:

- 由于 L2 上潜在的电路溢出而丢弃的消息将被跳过并且不被执行。自定义跨层调用合约需要实现
```onDropMessage```方法来考虑此类情况。

- 网关合约包含onDropMessage方法，旨在退还跨层消息的发起者。

- 通话```L1CrossDomainMessenger.dropMessage```丢弃跨层消息并触发原始合约中的 onDropMessage 方法，相应地将交易的值和消息作为 msg.value 和方法参数传递。
