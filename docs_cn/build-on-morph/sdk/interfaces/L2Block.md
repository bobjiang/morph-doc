[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/L2块

# Interface: L2Block

L2Geth 节点返回时的 JSON 块表示形式。只是一个普通的块，但带有
添加了 stateRoot 字段。

## Extends

-`Block`

## Properties

### \_difficulty

> **\_difficulty**: `BigNumber`

#### Inherited from

`Block._difficulty`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:41

***

### baseFeePerGas?

>`optional` **baseFeePerGas**: `BigNumber`

#### Inherited from

`Block.baseFeePerGas`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:46

***

### difficulty

> **difficulty**: `number`

#### Inherited from

`Block.difficulty`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:40

***

### extraData

> **extraData**: `string`

#### Inherited from

`Block.extraData`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:45

***

### gasLimit

> **gasLimit**: `BigNumber`

#### Inherited from

`Block.gasLimit`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:42

***

### gasUsed

> **gasUsed**: `BigNumber`

#### Inherited from

`Block.gasUsed`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:43

***

### hash

> **hash**: `string`

#### Inherited from

`Block.hash`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:35

***

### miner

> **miner**: `string`

#### Inherited from

`Block.miner`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:44

***

### nonce

> **nonce**: `string`

#### Inherited from

`Block.nonce`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:39

***

### number

> **number**: `number`

#### Inherited from

`Block.number`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:37

***

### parentHash

> **parentHash**: `string`

#### Inherited from

`Block.parentHash`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:36

***

### stateRoot

> **stateRoot**: `string`

#### Source

src/interfaces/l2-provider.ts:27

***

### timestamp

> **timestamp**: `number`

#### Inherited from

`Block.timestamp`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:38

***

### transactions

> **transactions**: `string`[]

#### Inherited from

`Block.transactions`

#### Source

node\_modules/@ethersproject/abstract-provider/lib/index.d.ts:49
