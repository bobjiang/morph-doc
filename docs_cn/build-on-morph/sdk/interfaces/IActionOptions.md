[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ IActionOptions

# Interface: IActionOptions

## Param

用于发送交易的可选签名者。

## Param

用于接收链上资金的可选地址。默认为发件人。

## Param

搜索消息的方向。如果未提供，将尝试
* 假设交易哈希只会自动搜索两个方向
* 存在于一条链上。如果哈希值在两条链上都存在，则会抛出错误。

## Param

可选的事务覆盖。

## Properties

### direction?

>`optional` **direction**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Source

src/interfaces/types.ts:412

***

### from?

>`optional` **from**: `string`

#### Source

src/interfaces/types.ts:410

***

### overrides?

>`optional` **overrides**: `object`&`CallOverrides`

#### Type declaration

##### gatewayAddress?

>`optional` **gatewayAddress**: `string`

##### gatewayName?

>`optional` **gatewayName**: `string`

#### Source

src/interfaces/types.ts:413

***

### recipient?

>`optional` **recipient**: [`AddressLike`](../type-aliases/AddressLike.md)

#### Source

src/interfaces/types.ts:411

***

### signer?

>`optional` **signer**: `Signer`

#### Source

src/interfaces/types.ts:409
