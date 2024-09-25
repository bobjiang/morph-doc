---
title: Morph 和以太坊的区别
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---

以太坊的 EVM 和 Morph 的乐观 zkEVM 之间存在一些技术差异。我们编制了一个列表来帮助您更好地理解这些区别。


:::tip
对于大多数 Solidity 开发人员来说，这些技术细节不会显着影响您的开发体验。
:::

## EVM Opcodes


|操作码|坚固度等效 |变形行为 |
| --------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------- |
|`BLOCKHASH`|`block.blockhash`|退货`keccak(chain_id \|\| block_number)`最后 256 个区块。                                      |
|`COINBASE`|`block.coinbase`|返回预先部署的费用保险库合约地址。看[Contracts](../../build-on-morph/developer-resources/1-contracts.md). |
|`DIFFICULTY`/`PREVRANDAO`|`block.difficulty`|返回 0。
|`BASEFEE`|`block.basefee`|残疾人。如果遇到操作码，事务将被恢复。                        |
|`SELFDESTRUCT`|`selfdestruct`|残疾人。如果遇到操作码，事务将被恢复。                     |

## EVM Precompiles

这`RIPEMD-160`（地址`0x3`)`blake2f`（地址`0x9`）， 和`point evaluation`（地址`0x0a`) 目前不支持预编译。对不受支持的预编译合约的调用将恢复。我们计划在未来的硬分叉中启用这些预编译。

这`modexp`支持预编译，但仅支持大小小于或等于 32 字节的输入（即`u256`).

这`ecPairing`支持预编译，但点数（集、对）限制为 4，而不是 6。

The other EVM precompiles are all supported: `ecRecover`,`identity`,`ecAdd`,`ecMul`.

### Precompile Limits

由于 zkEVM 电路的大小有限，因此某些预编译可以进行的调用数量存在上限。这些事务不会恢复，但如果无法放入电路空间，则只会被定序器跳过。

|预编译/操作码 |限制|
| ------------------- | ----- |
|`keccak256`| 3157  |
|`ecRecover`| 119   |
|`modexp`| 23    |
|`ecAdd`| 50    |
|`ecMul`| 50    |
|`ecPairing`| 2     |

:::tipDencun 升级操作码不可用

Morph 上尚未提供 Dencun 升级的操作码，包括`MCOPY`,`TSTORE`,`TLOAD`,`BLOBHASH`和`BLOBBASEFEE`。此外，[EIP-4788](https://eips.ethereum.org/EIPS/eip-4788)不支持访问信标链块根。我们建议使用`shanghai`作为您的 EVM 目标并避免使用高于`0.8.23`.

:::

## State Account

### **Additional Fields**

我们在当前的内容中添加了两个字段`StateAccount` object: `PoseidonCodehash`和`CodeSize`.

```go
type StateAccount struct {
	Nonce    uint64
	Balance  *big.Int
	Root     common.Hash // merkle root of the storage trie
	KeccakCodeHash []byte // still the Keccak codehash
	// added fields
	PoseidonCodeHash []byte // the Poseidon codehash
	CodeSize uint64
}
```

### **CodeHash**

Related to this, we maintain two types of codehash for each contract bytecode: Keccak hash and Poseidon hash.

`KeccakCodeHash`保留以保持兼容性`EXTCODEHASH`.`PoseidonCodeHash`用于验证 zkEVM 中加载的字节码的正确性，其中 Poseidon 哈希效率更高。

### CodeSize

验证时`EXTCODESIZE`，将整个合约数据加载到 zkEVM 中的成本很高。相反，我们在合约创建期间将合约大小存储在存储中。这样，我们不需要加载代码——存储证明足以验证这个操作码。

## Block Time

:::tip区块时间可能会发生变化

每秒产生一个块，如果5秒内没有交易，则生成一个空块。然而，这个频率将来可能会改变。
:::

相比之下，以太坊的出块时间约为 12 秒。

Morph 出块时间更快的原因
User Experience: 

- 更快、一致的出块时间提供更快的反馈，增强用户体验。

- Optimization: As we refine the zkEVM circuits in our testnets, we can achieve higher throughput than Ethereum, even with a smaller gas limit per block or batch.


Notice:
-`TIMESTAMP`将返回块的时间戳。它每秒都会更新。
-`BLOCKNUMBER`将返回实际的块号。它每秒都会更新。区块和交易之间的一对一映射将不再适用。




<!--
We also introduce the concept of system transactions that are created by the `op-node`, and are used to execute deposits and update the L2's view of L1. They have the following attributes:

- Every block will contain at least one system transaction called the L1 attributes deposited transaction. It will always be the first transaction in the block.
- Some blocks will contain one or more user-deposited transactions.
- All system transactions have an [EIP-2718](https://eips.ethereum.org/EIPS/eip-2718)-compatible transaction type of `0x7E`.
- All system transactions are unsigned, and set their `v`, `r`, and `s` fields to `null`.


:::Warning Known Issue
Some Ethereum client libraries, such as Web3js, cannot parse the `null` signature fields described above. To work around this issue, you will need to manually filter out the system transactions before passing them to the library. 
:::
-->

## Future EIPs

Morph 密切关注新兴的以太坊改进提案（EIP），并在合适的时候采用它们。如需了解更多详情，请加入我们的社区论坛或[Discord](https://discord.gg/L2Morph)供讨论。

<!-- ## EVM Target version 

To avoid unexpected behaviors in your contracts, we recommend using ‘london’ as the target version when compiling your smart contracts.

You can read in more details on Shanghai hard fork differences from London on the [Ethereum Execution spec](https://github.com/ethereum/execution-specs/tree/master/network-upgrades/mainnet-upgrades/shanghai.md) and how the new PUSH0 instruction [impacts the Solidity compiler](https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/).
-->

