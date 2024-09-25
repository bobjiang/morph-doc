[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ L2BlockWithTransactions

# Interface: L2BlockWithTransactions

L2Geth 节点返回时的 JSON 块表示形式。只是一个普通的块，但带有
L2Transaction 对象而不是标准事务响应对象。

## Extends

-`BlockWithTransactions`

## Properties

### \_difficulty

> **\_difficulty**: `BigNumber`

#### Inherited from

`BlockWithTransactions._difficulty`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:41

***

### baseFeePerGas?

>`optional` **baseFeePerGas**: `BigNumber`

#### Inherited from

`BlockWithTransactions.baseFeePerGas`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:46

***

### difficulty

> **difficulty**: `number`

#### Inherited from

`BlockWithTransactions.difficulty`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:40

***

### extraData

> **extraData**: `string`

#### Inherited from

`BlockWithTransactions.extraData`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:45

***

### gasLimit

> **gasLimit**: `BigNumber`

#### Inherited from

`BlockWithTransactions.gasLimit`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:42

***

### gasUsed

> **gasUsed**: `BigNumber`

#### Inherited from

`BlockWithTransactions.gasUsed`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:43

***

### hash

> **hash**: `string`

#### Inherited from

`BlockWithTransactions.hash`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:35

***

### miner

> **miner**: `string`

#### Inherited from

`BlockWithTransactions.miner`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:44

***

### nonce

> **nonce**: `string`

#### Inherited from

`BlockWithTransactions.nonce`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:39

***

### number

> **number**: `number`

#### Inherited from

`BlockWithTransactions.number`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:37

***

### parentHash

> **parentHash**: `string`

#### Inherited from

`BlockWithTransactions.parentHash`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:36

***

### stateRoot

> **stateRoot**: `string`

#### Source

src/interfaces/l2-provider.ts:35

***

### timestamp

> **timestamp**: `number`

#### Inherited from

`BlockWithTransactions.timestamp`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:38

***

### transactions

> **transactions**: [[`L2Transaction`](L2Transaction.md)]

#### Overrides

`BlockWithTransactions.transactions`

#### Source

src/interfaces/l2-provider.ts:36
