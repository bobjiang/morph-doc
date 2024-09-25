---
title: 了解 Morph 上的交易成本
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


Morph 上的交易费用与以太坊上的费用类似。然而，第 2 层引入了一些独特的方面。 Morph 乐观的 zkEVM 使这些差异变得容易理解，甚至更容易处理。

此页面包含计算 Morph 上交易的 Gas 成本的公式。
There are two kinds of costs for transactions on Morph: the L2 execution fee and the L1 data/security fee.


<!--
:::tip

The transaction fees are collected into the `SequencerFeeVault` contract balance. This contract also tracks the amount we’ve historically withdrawn to L1 using `totalProcessed()(uint256)`.

The block producer receives no direct reward, and the `COINBASE` opcode returns the fee vault address.

:::
-->

## The L2 execution fee

与以太坊一样，Morph 上的交易会产生用于计算和存储使用的 Gas 成本。

每笔 L2 交易都会支付一些**执行**费用，等于使用的 Gas 量乘以交易的 Gas 价格。

Morph 支持 EIP-1559 交易类型。 EIP-1559定价模型由基本费用和优先费用组成，有助于提高交易费用的可预测性和稳定性。

The formula is straightforward:
```
l2_execution_fee = l2_gas_price * l2_gas_used
l2_gas_price = l2_base_fee + l2_priority_fee
```

L2 Gas 的使用量取决于具体交易。由于 EVM 兼容性，Morph 上的 Gas 使用量通常与以太坊类似。


## The L1 data fee

Morph 交易也发布到以太坊，这对 Morph 的安全性至关重要，因为它确保验证 Morph 状态所需的所有数据始终在以太坊上公开可用。

用户必须支付向以太坊提交交易的费用，称为 L1 数据费。该费用通常占 Morph 交易总成本的大部分。

Formula:

```
l1DataFee = (l1BaseFee * commitScalar + l1BlobBaseFee * tx_data_gas * blobScalar) / rcfg.Precision
```

其中 tx_data_gas 是

```
tx_data_gas = count_zero_bytes(tx_data) * 4 + count_non_zero_bytes(tx_data) * 16
```

以及其他参数：

1. l1BaseFee：Layer1基础费用
2. commitScalar：用于衡量数据提交的gas成本的因子
3. l1BlobBaseFee：L1上的blobBaseFee
4. blobScalar：用于衡量一笔交易存储在EIP-4844 blob中的gas成本的因子


:::tip
您可以从 GasPrice 预言机合约中读取参数值。 Morph已预先部署`GasPriceOracle`，可在 Morph Holesky 上访问[GasPriceOracle](https://explorer-holesky.morphl2.io/address/0x530000000000000000000000000000000000000F).
:::



## Transaction fees' effect on software development

### Sending transactions

在 Morph 上发送交易的过程与在以太坊上发送交易的过程相同。

发送交易时，您应提供大于或等于当前 L2 Gas 价格的 Gas 价格。

就像在以太坊上一样，您可以使用以下命令查询汽油价格`eth_gasPrice`RPC方法。

同样，您应该以与在以太坊上设置相同的方式设置交易气体限制（例如通过`eth_estimateGas`).


### Displaying fees to users

许多以太坊应用程序通过将 Gas 价格乘以 Gas 限制来向用户显示估计费用。

然而，如前所述，Morph 上的用户需要支付 L2 执行费和 L1 数据费。

因此，您应该显示这两项费用的总和，以便用户能够最准确地估计交易的总成本。


#### Estimating the L2 execution fee

您可以通过将 Gas 价格乘以 Gas 限制来估算 L2 执行费用，就像在以太坊上一样。

#### [Estimating the L1 data fee](./understand-transaction-cost-on-morph#the-l1-data-fee)



#### Estimating the total fee

您可以通过结合 L2 执行费用和 L1 数据费用的估算来估算总费用。

### Sending max ETH

发送用户钱包中最大数量的 ETH 是一个相对常见的用例。

执行此操作时，您需要从您希望用户发送的 ETH 金额中减去估计的 L2 执行费用和估计的 L1 数据费用。

使用上述逻辑来估算总费用。

## Common RPC Errors

### Insufficient funds

- Error code: `-32000`
- Error message: `invalid transaction: insufficient funds for l1Fee + l2Fee + value`

当您尝试发送交易并且您没有足够的 ETH 来支付交易价值、L2 执行费和 L1 数据费时，您会收到此错误。
如果您没有正确考虑 L2 执行费用和 L1 数据费用，则在尝试发送最大 ETH 时可能会收到此错误。

### Gas price too low

- Error code: `-32000`
- Error message: `gas price too low: X wei, use at least tx.gasPrice = Y wei`

这是一个自定义 RPC 错误，当交易因 Gas 价格太低而被拒绝时，Morph 会返回该错误。
请参阅有关部分[Responding to gas price updates](#responding-to-gas-price-updates)了解更多信息。

### Gas price too high
- Error code: `-32000`
- Error message: `gas price too high: X wei, use at most tx.gasPrice = Y wei`

这是一个自定义 RPC 错误，当交易因 Gas 价格太高而被拒绝时，Morph 会返回该错误。
我们将此作为一项安全措施，以防止用户意外发送具有极高 L2 Gas 价格的交易。
请参阅有关的部分[Responding to gas price updates](#responding-to-gas-price-updates)了解更多信息。