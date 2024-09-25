[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 省略

# Function: omit()

> **省略**\<`T`, `K`\>(`obj`, ...`keys`): `Omit`\<`T`, `K`\>

返回给定对象 ( ...obj ) 的副本，并省略给定键。

## Type parameters

• **T** *延伸*`object`

• **K** *延伸*`string`\|`number`\|`symbol`

## Parameters

• **obj**: `T`

要返回的对象，但省略了键。

• ...**keys**: `K`[]

要从返回的对象中省略的键。

## Returns

`Omit`\<`T`, `K`\>

给定对象的副本，省略给定键。

## Source

src/utils/misc-utils.ts:11
