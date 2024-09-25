[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 到签名者或提供者

# Function: toSignerOrProvider()

> **到签名者或提供者**(`signerOrProvider`): `Provider`\|`Signer`

将 SignerOrProviderLike 转换为 Signer 或 Provider。假设如果输入是
string 那么它是一个 JSON-RPC url。

## Parameters

• **signerOrProvider**: [`SignerOrProviderLike`](../type-aliases/SignerOrProviderLike.md)

SignerOrProviderLike 成为签名者或提供者。

## Returns

`Provider`\|`Signer`

作为签名者或提供者输入。

## Source

src/utils/coercion.ts:25
