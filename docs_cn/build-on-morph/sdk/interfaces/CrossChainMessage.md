[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 跨链消息

# Interface: CrossChainMessage

描述在 L1 和 L2 之间发送的消息。方向决定消息的位置
发送来源和发送目的地。

## Extends

-[`CoreCrossChainMessage`](CoreCrossChainMessage.md)

## Properties

### blockNumber

> **blockNumber**: `number`

#### Source

src/interfaces/types.ts:255

***

### direction

> **direction**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Source

src/interfaces/types.ts:253

***

### logIndex

> **logIndex**: `number`

#### Source

src/interfaces/types.ts:254

***

### message

> **message**: `string`

#### Inherited from

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`message`](CoreCrossChainMessage.md#message)

#### Source

src/interfaces/types.ts:242

***

### messageNonce

> **messageNonce**: `BigNumber`

#### Inherited from

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`messageNonce`](CoreCrossChainMessage.md#messagenonce)

#### Source

src/interfaces/types.ts:243

***

### minGasLimit

> **minGasLimit**: `BigNumber`

#### Inherited from

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`minGasLimit`](CoreCrossChainMessage.md#mingaslimit)

#### Source

src/interfaces/types.ts:245

***

### sender

> **sender**: `string`

#### Inherited from

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`sender`](CoreCrossChainMessage.md#sender)

#### Source

src/interfaces/types.ts:240

***

### target

> **target**: `string`

#### Inherited from

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`target`](CoreCrossChainMessage.md#target)

#### Source

src/interfaces/types.ts:241

***

### transactionHash

> **transactionHash**: `string`

#### Source

src/interfaces/types.ts:256

***

### value

> **value**: `BigNumber`

#### Inherited from

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`value`](CoreCrossChainMessage.md#value)

#### Source

src/interfaces/types.ts:244
