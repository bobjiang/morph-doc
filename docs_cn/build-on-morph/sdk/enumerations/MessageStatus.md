[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 消息状态

# Enumeration: MessageStatus

描述消息状态的枚举。

## Enumeration Members

### FAILED\_L1\_TO\_L2\_MESSAGE

> **FAILED\_L1\_TO\_L2\_MESSAGE**: `1`

消息是 L1 到 L2 消息，执行该消息的事务失败。
当返回此状态时，您将需要重新发送 L1 到 L2 消息，可能带有
更高的气体限制。

#### Source

src/interfaces/types.ts:186

***

### IN\_CHALLENGE\_PERIOD

> **IN\_CHALLENGE\_PERIOD**: `5`

消息是经过验证的 L2 到 L1 消息，正在经历挑战期。

#### Source

src/interfaces/types.ts:206

***

### READY\_FOR\_RELAY

> **READY\_FOR\_RELAY**: `6`

消息已准备好转发。

#### Source

src/interfaces/types.ts:211

***

### READY\_TO\_PROVE

> **READY\_TO\_PROVE**: `4`

消息已准备好在 L1 上进行证明以启动挑战期。

#### Source

src/interfaces/types.ts:201

***

### RELAYED

> **RELAYED**: `7`

消息已转发。

#### Source

src/interfaces/types.ts:216

***

### UNCONFIRMED\_L1\_TO\_L2\_MESSAGE

> **UNCONFIRMED\_L1\_TO\_L2\_MESSAGE**: `0`

消息是L1到L2的消息，并且没有经过L2处理。

#### Source

src/interfaces/types.ts:179

***

### WITHDRAWAL\_HASH\_NOT\_SYNC

> **WITHDRAWAL\_HASH\_NOT\_SYNC**: `3`

消息是 L2 到 L1 消息，提款哈希尚未发布到后端。

#### Source

src/interfaces/types.ts:196

***

### WITHDRAWAL\_ROOT\_NOT\_PUBLISHED

> **WITHDRAWAL\_ROOT\_NOT\_PUBLISHED**: `2`

消息是L2到L1消息，提现根尚未发布。

#### Source

src/interfaces/types.ts:191
