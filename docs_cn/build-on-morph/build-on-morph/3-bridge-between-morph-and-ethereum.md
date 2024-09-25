---
title: Morph 和以太坊之间的桥梁
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


请首先查看我们的文档[Communication Between Morph and Ethereum](../../how-morph-works/general-protocol-design/2-communicate-between-morph-and-ethereum.md)一些需要的基础知识。


## Deposit ETH and ERC20 Tokens from L1​

网关路由器允许分别使用 DepositETH 和 DepositERC20 函数将 ETH 和 ERC20 代币从 L1 桥接到 L2。它是部署在 L1 上的无需许可的网桥。请注意，ERC20 代币在 L2 上将具有不同的地址，您可以使用 getL2ERC20Address 函数查询新地址。

:::tip
**`depositETH`** 和 **`depositERC20`** 是付费函数，发送到这些函数的 ETH 数量将被使用
支付L2费用。如果金额不足，交易将不会发送。所有多余的 ETH 将被发送回发件人。`0.00001 ETH`应该足以处理代币存款。
:::

桥接 ERC20 代币时，您不必担心选择正确的网关。这是因为`L1GatewayRouter` 将选择正确的底层入口点来发送消息:

-**`L1StandardERC20Gateway`:**该网关允许任何 ERC20 存款，并且将被 L1GatewayRouter 选择为不需要在 L2 上自定义逻辑的 ERC20 代币的默认网关。在第一个代币桥接时，将在 L2 上创建一个实现 MorphStandardERC20 的新代币。要桥接令牌，请调用`depositERC20`函数在`L1GatewayRouter`.

<!---->
<!--
- **`L1CustomERC20Gateway`:** This Gateway will be selected by the `L1GatewayRouter` for tokens with custom logic. For an L1/L2 token pair to work on the Morph Custom ERC20 Bridge, the L2 token contract has to implement `IMorphStandardERC20`. Additionally, the token should grant `mint` or `burn` capability to the `L2CustomERC20Gateway`. 
-->

所有网关合约都会形成消息并将其发送到`L1CrossDomainMessenger`它可以向 L2 发送任意消息。这`L1CrossDomainMessenger`将消息传递给`L1MessageQueueWithGasPriceOracle`。任何用户都可以直接向 Messenger 发送消息，在 L2 上执行任意数据。

这意味着他们可以通过网桥在 L1 上进行的交易执行 L2 上的任何功能。尽管应用程序可以直接将消息传递到现有的代币合约，但网关抽象了细节并简化了传输和调用。

当 L1 上创建新块时，Sequencer 将检测 L1 上的消息`L1MessageQueue`，并通过L2节点将交易提交给L2。最后，L2节点将交易传递给`L2CrossDomainMessenger`在 L2 上执行的合约。

## Withdraw ETH and ERC20 tokens from L2

L2 网关与 L1 网关非常相似。我们可以使用以下命令将 ETH 和 ERC20 代币提取回 L1：`withdrawETH`和`withdrawERC20`功能。合约地址部署在L2上。我们使用`getL1ERC20Address`检索 L1 上的令牌地址。

:::tip
**`withdrawETH`** 和 **`withdrawERC20`** 是付费函数，发送到这些函数的 ETH 数量将用于支付 L1 费用。如果金额不足，交易将不会发送。所有多余的 ETH 将被发送回发送者。费用将取决于 L1 活动，但`0.005 ETH`应该足以处理代币取款。
:::

:::tip
**确保从 L2 发送时交易不会在 L1 上恢复** 如果您的交易在 L1 上恢复，则无法恢复桥接的 ETH、代币或 NFT。当交易发送时，所有资产都会在 Morph 上被烧毁，并且不可能再次铸造它们。
:::

### Finalize your Withdrawal

除了在 Morph 上发起提款请求外，还需要执行一个额外步骤。您需要在以太坊上完成提款。

这是因为Morph乐观的zkEVM设计，你可以阅读详细信息[here](../../how-morph-works/general-protocol-design/2-communicate-between-morph-and-ethereum.md): 



为了完成这个, 首先你要确认:

- 包含提款交易的批次已通过挑战期并标记为最终确定（意味着在`Rollup`合同，**withdrawalRoots[batchDataStore[_batchIndex].withdrawalRoot] = true**）。

一旦确认，您可以调用我们的后端服务接口：

`/getProof?nonce=withdraw.index`

获取完成提款所需的所有信息，包括：

- 索引：提款交易在提款树中的位置，或您的交易在所有 L2->L1 交易中的排名。
- 叶：存储在树中的提款交易的哈希值。
- 证明：您的提款交易的默克尔证明。
- 根：提款树根。


你需要使用`proveAndRelayMessage`的功能`L1CrossDomainMessenger`合同。

获得上述信息后，可以通过调用来完成提现操作`L1CrossDomainMessenger.proveAndRelayMessage()`.

所需的参数是

```solidity
  address _from, 
  address _to, 
  uint256 _value, 
  uint256 _nonce, 
  bytes memory _message, 
  bytes32[32] calldata _withdrawalProof, 
  bytes32 _withdrawalRoot
```

`_from`,`_to`,`_value`,`_nonce`， 和`_message`是提现交易的原始内容，可以从活动中获取`SentMessage`包含在L2层提现发起的交易中。

`_withdrawalProof`和`_withdrawalRoot`可以从前述后端API接口获取。

<!--

## Creating an ERC20 token with custom logic on L2

If a token needs custom logic on L2, it will need to be bridged through an `L1CustomERC20Gateway` and `L2CustomERC20Gateway` respectively. The custom token on L2 will need to give permission to the Gateway to mint new tokens when a deposit occurs and to burn when tokens are withdrawn

The following interface is the `IMorphStandardERC20` needed for deploying tokens compatible with the `L2CustomERC20Gateway` on L2.

```solidity
interface IMorphStandardERC20 {
  /// @notice Return the address of Gateway the token belongs to.
  function gateway() external view returns (address);

  /// @notice Return the address of counterpart token.
  function counterpart() external view returns (address);

  /// @dev ERC677 Standard, see https://github.com/ethereum/EIPs/issues/677
  /// Defi can use this method to transfer L1/L2 token to L2/L1,
  /// and deposit to L2/L1 contract in one transaction
  function transferAndCall(address receiver, uint256 amount, bytes calldata data) external returns (bool success);

  /// @notice Mint some token to recipient's account.
  /// @dev Gateway Utilities, only gateway contract can call
  /// @param _to The address of recipient.
  /// @param _amount The amount of token to mint.
  function mint(address _to, uint256 _amount) external;

  /// @notice Burn some token from account.
  /// @dev Gateway Utilities, only gateway contract can call
  /// @param _from The address of account to burn token.
  /// @param _amount The amount of token to mint.
  function burn(address _from, uint256 _amount) external;
}
```

### Adding a Custom L2 ERC20 token to the Morph Bridge

Tokens can be bridged securely and permissionlessly through Gateway contracts deployed by any developer. However, Morph also manages an ERC20 Router and a Gateway where all tokens created by the community are welcome. Being part of the Morph-managed Gateway means you won't need to deploy the Gateway contracts, and your token will appear in the Morph frontend. To be part of the Morph Gateway, you must contact the Morph team to add the token to both L1 and L2 bridge contracts. To do so, follow the instructions on the [token lists](https://github.com/Morph-tech/token-list) repository to add your new token to the official Morph frontend.

-->

:::tip
使用SDK

您也可以尝试我们的SDK与桥接系统交互，参考我们的[SDK Doc](../sdk/globals.md).

:::
## Add your Token to the Official Bridge

目前，我们的官方桥接仅支持某些预定义的令牌进行桥接。如果您想桥接自己的令牌，则需要手动添加令牌，以下是操作方法。

### Add Tokens to the gateway through Morph Bridge Frontend

支持您的令牌的最简单方法是将其手动添加到我们的[official bridge frontend](https://bridge-holesky.morphl2.io/), you can simply do it with the following steps:

1. 单击 Morph Holesky Bridge 上的代币选择按钮

![tokenlist1](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist1.png)


2. 在自定义代币部分输入并确认您想要的以太坊代币合约地址

![tokenlist2](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist2.png)

3. 获取二层代币合约地址并确认。

![tokenlist3](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist3.png)

4. 现在它已受支持，您和其他用户可以开始桥接它！

![tokenlist4](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist4.png)

### Add token support to the bridge frontend

通过将您的令牌添加到网关，您和其他用户可以通过输入令牌地址来桥接令牌。如果您希望您的令牌显示在桥接前端令牌列表中，则需要向我们的桥接存储库提出 PR。

您可以在中找到如何操作[morph list repo](https://github.com/morph-l2/morph-list).


Keep in mind that:
- 您需要将 L1 和 L2 令牌添加到列表中。
- L2代币合约地址是通过Morph桥前端添加您的代币获得的。

这是一个 [示例 PRcommit](https://github.com/morph-l2/morph-list/pull/27/commits/228481db6b8d69b8f40e7369dae62722aa570eb7)供您参考。




