---
title: 使用SDK与Morph交互
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---



**@morph-l2/sdk** •[**Docs**](globals.md)

***

# @morph-l2/sdk

这`@morph-l2/sdk`软件包提供了一组与 Morph 交互的工具。

## Installation

```
npm install @morph-l2/sdk@latest
```

## Docs

您可以在以下位置找到自动生成的 API 文档[docs.morphl2.io](https://docs.morphl2.io/docs/build-on-morph/sdk/globals/).

## Using the SDK

### CrossChainMessenger

这[`CrossChainMessenger`](https://docs.morphl2.io/docs/build-on-morph/sdk/classes/CrossChainMessenger)类简化了在以太坊和 Morph 之间移动资产和数据的过程。
例如，您可以使用此类启动将 ERC20 代币从 Morph 提现回以太坊，准确跟踪提现何时准备好在以太坊上完成，并在挑战期结束后执行最终确定交易。
这`CrossChainMessenger`可以处理 ETH 和任何 ERC20 兼容代币的存款和取款。
这`CrossChainMessenger`自动连接到所有相关合约，因此不需要复杂的配置。

### L2Provider and related utilities

Morph SDK 包括[various utilities](https://docs.morphl2.io/docs/build-on-morph/sdk/type-aliases/L2Provider)用于处理 Morph 的[transaction fee model](https://docs.morphl2.io/docs/build-on-morph/build-on-morph/understand-transaction-cost-on-morph/).
例如，[`estimateTotalGasCost`](https://docs.morphl2.io/docs/build-on-morph/sdk/functions/estimateTotalGasCost)将估计在 Morph 上发送交易的总成本（以 wei 为单位），包括 L2 执行成本和 L1 数据成本。
您还可以使用[`asL2Provider`](https://docs.morphl2.io/docs/build-on-morph/sdk/functions/asL2Provider)函数将 ethers Provider 对象包装成`L2Provider`它将附加所有这些辅助函数。

### Other utilities

SDK 包含其他有用的辅助函数和常量。
有关完整列表，请参阅自动生成的[SDK documentation](https://docs.morphl2.io/docs/build-on-morph/sdk/globals/)


## Documents
### Enumerations

-[L1ChainID](enumerations/L1ChainID.md)
-[L1RpcUrls](enumerations/L1RpcUrls.md)
-[L2ChainID](enumerations/L2ChainID.md)
-[L2RpcUrls](enumerations/L2RpcUrls.md)
-[MessageDirection](enumerations/MessageDirection.md)
-[MessageReceiptStatus](enumerations/MessageReceiptStatus.md)
-[MessageStatus](enumerations/MessageStatus.md)

### Classes

-[CrossChainMessenger](classes/CrossChainMessenger.md)
-[ETHBridgeAdapter](classes/ETHBridgeAdapter.md)
-[StandardBridgeAdapter](classes/StandardBridgeAdapter.md)

### Interfaces

-[BridgeAdapterData](interfaces/BridgeAdapterData.md)
-[BridgeAdapters](interfaces/BridgeAdapters.md)
-[CoreCrossChainMessage](interfaces/CoreCrossChainMessage.md)
-[CrossChainMessage](interfaces/CrossChainMessage.md)
-[CrossChainMessageRequest](interfaces/CrossChainMessageRequest.md)
-[IActionOptions](interfaces/IActionOptions.md)
-[IBridgeAdapter](interfaces/IBridgeAdapter.md)
-[L2Block](interfaces/L2Block.md)
-[L2BlockWithTransactions](interfaces/L2BlockWithTransactions.md)
-[L2Transaction](interfaces/L2Transaction.md)
-[MessageReceipt](interfaces/MessageReceipt.md)
-[OEContracts](interfaces/OEContracts.md)
-[OEContractsLike](interfaces/OEContractsLike.md)
-[OEL1Contracts](interfaces/OEL1Contracts.md)
-[OEL2Contracts](interfaces/OEL2Contracts.md)
-[ProvenWithdrawal](interfaces/ProvenWithdrawal.md)
-[StateRoot](interfaces/StateRoot.md)
-[StateRootBatch](interfaces/StateRootBatch.md)
-[StateRootBatchHeader](interfaces/StateRootBatchHeader.md)
-[TokenBridgeMessage](interfaces/TokenBridgeMessage.md)
-[WithdrawMessageProof](interfaces/WithdrawMessageProof.md)
-[WithdrawalEntry](interfaces/WithdrawalEntry.md)

### Type Aliases

-[AddressLike](type-aliases/AddressLike.md)
-[DeepPartial](type-aliases/DeepPartial.md)
-[L1Provider](type-aliases/L1Provider.md)
-[L2Provider](type-aliases/L2Provider.md)
-[LowLevelMessage](type-aliases/LowLevelMessage.md)
-[MessageLike](type-aliases/MessageLike.md)
-[MessageRequestLike](type-aliases/MessageRequestLike.md)
-[NumberLike](type-aliases/NumberLike.md)
-[OEL1ContractsLike](type-aliases/OEL1ContractsLike.md)
-[OEL2ContractsLike](type-aliases/OEL2ContractsLike.md)
-[ProviderLike](type-aliases/ProviderLike.md)
-[SignerLike](type-aliases/SignerLike.md)
-[SignerOrProviderLike](type-aliases/SignerOrProviderLike.md)
-[TransactionLike](type-aliases/TransactionLike.md)

### Variables

-[BRIDGE\_ADAPTER\_DATA](variables/BRIDGE_ADAPTER_DATA.md)
-[CHAIN\_BLOCK\_TIMES](variables/CHAIN_BLOCK_TIMES.md)
-[CONTRACT\_ADDRESSES](variables/CONTRACT_ADDRESSES.md)
-[DEFAULT\_L1\_CONTRACT\_ADDRESSES](variables/DEFAULT_L1_CONTRACT_ADDRESSES.md)
-[DEFAULT\_L2\_CONTRACT\_ADDRESSES](variables/DEFAULT_L2_CONTRACT_ADDRESSES.md)
-[DEPOSIT\_CONFIRMATION\_BLOCKS](variables/DEPOSIT_CONFIRMATION_BLOCKS.md)
-[l1BridgeName](variables/l1BridgeName.md)
-[l1CrossDomainMessengerName](variables/l1CrossDomainMessengerName.md)
-[l2BridgeName](variables/l2BridgeName.md)
-[l2CrossDomainMessengerName](variables/l2CrossDomainMessengerName.md)

### Functions

-[asL2Provider](functions/asL2Provider.md)
-[estimateL1Gas](functions/estimateL1Gas.md)
-[estimateL1GasCost](functions/estimateL1GasCost.md)
-[estimateL2GasCost](functions/estimateL2GasCost.md)
-[estimateTotalGasCost](functions/estimateTotalGasCost.md)
-[getAllOEContracts](functions/getAllOEContracts.md)
-[getBridgeAdapters](functions/getBridgeAdapters.md)
-[getL1GasPrice](functions/getL1GasPrice.md)
-[getOEContract](functions/getOEContract.md)
-[hashLowLevelMessageV2](functions/hashLowLevelMessageV2.md)
-[hashMessageHash](functions/hashMessageHash.md)
-[isL2Provider](functions/isL2Provider.md)
-[migratedWithdrawalGasLimit](functions/migratedWithdrawalGasLimit.md)
-[omit](functions/omit.md)
-[toAddress](functions/toAddress.md)
-[toBigNumber](functions/toBigNumber.md)
-[toNumber](functions/toNumber.md)
-[toProvider](functions/toProvider.md)
-[toSignerOrProvider](functions/toSignerOrProvider.md)
-[toTransactionHash](functions/toTransactionHash.md)
