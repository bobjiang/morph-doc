---
title: Morph 和以太坊之间的桥梁
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


## Bridge an ERC20 through custom gateway


## Step 1: Launch a token on Holesky

首先，我们需要一个令牌来桥接。代币无需特定的 ERC20 实现即可与 L2 兼容。如果您已经有令牌，请随意跳过此步骤。如果您想部署新代币，请使用以下简单 ERC20 代币合约，该合约在启动时会向部署者铸造 100 万个代币。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract L1Token is ERC20 {
  constructor() ERC20("My Token L1", "MTL1") {
    _mint(msg.sender, 1_000_000 ether);
  }
}
```

## Step 2: Launch the counterpart token on Morph Holesky testnet

接下来，您将在 Morph 上启动此代币的对应项，它将代表 Holesky 上的原始代币。该代币可以实现自定义逻辑以匹配 L1 代币的逻辑，甚至添加 L1 代币之外的其他功能。

For this to work:

- 代币必须实现`IMorphStandardERC20`接口以与桥兼容。
- 合约应提供网关地址和对应代币地址（我们刚刚推出的L1代币）`gateway()`和`counterpart()`功能。它还应该允许 L2 网关调用令牌`mint()`和`burn()`函数，在存入和提取代币时调用。

以下是与桥兼容的令牌的完整示例。您将向构造函数传递官方 Morph 自定义网关地址（`0x058dec71E53079F9ED053F3a0bBca877F6f3eAcf`）以及 Holesky 上启动的代币地址。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@Morph-tech/contracts@0.1.0/libraries/token/IMorphERC20Extension.sol";

contract L2Token is ERC20, IMorphERC20Extension {
  // We store the gateway and the L1 token address to provide the gateway() and counterpart() functions which are needed from the Morph Standard ERC20 interface
  address _gateway;
  address _counterpart;

  // In the constructor we pass as parameter the Custom L2 Gateway and the L1 token address as parameters
  constructor(address gateway_, address counterpart_) ERC20("My Token L2", "MTL2") {
    _gateway = gateway_;
    _counterpart = counterpart_;
  }

  function gateway() public view returns (address) {
    return _gateway;
  }

  function counterpart() external view returns (address) {
    return _counterpart;
  }

  // We allow minting only to the Gateway so it can mint new tokens when bridged from L1
  function transferAndCall(address receiver, uint256 amount, bytes calldata data) external returns (bool success) {
    transfer(receiver, amount);
    data;
    return true;
  }

  // We allow minting only to the Gateway so it can mint new tokens when bridged from L1
  function mint(address _to, uint256 _amount) external onlyGateway {
    _mint(_to, _amount);
  }

  // Similarly to minting, the Gateway is able to burn tokens when bridged from L2 to L1
  function burn(address _from, uint256 _amount) external onlyGateway {
    _burn(_from, _amount);
  }

  modifier onlyGateway() {
    require(gateway() == _msgSender(), "Ownable: caller is not the gateway");
    _;
  }
}
```

## Step 3: Add the token to the Morph Bridge

您需要联系 Morph 团队将代币添加到`L2CustomERC20Gateway`Morph 中的合约和`L1CustomERC20Gateway`L1 中的合同。此外，请按照[token lists](https://github.com/Morph-tech/token-list)存储库将您的令牌添加到 Morph 官方网桥前端。

## Step 4: Deposit tokens

一旦您的代币获得 Morph 团队的批准，您应该能够从 L1 存入代币。为此，您必须首先批准`L1CustomGateway`Holesky 上的合约地址（`0x31C994F2017E71b82fd4D8118F140c81215bbb37`）。然后，通过调用存入代币`depositERC20`函数从`L1CustomGateway`合同。这可以使用以下方法完成[our bridge UI](https://Morph.io/bridge),[Etherscan Holesky](https://Holesky.etherscan.io/address/0x31C994F2017E71b82fd4D8118F140c81215bbb37#writeProxyContract)，或智能合约。

## Step 5: Withdraw tokens

您将按照类似的步骤将令牌从 L2 发送回 L1。首先，批准`L2CustomGateway`地址 （`0x058dec71E53079F9ED053F3a0bBca877F6f3eAcf`），然后调用调用提取代币`withdrawERC20`从`L2CustomGateway`合同。


## Send messages between Morph and Ethereum

## Deploying the Contracts

### Target Smart Contract

让我们从部署目标智能合约开始。我们将为此使用 Greeter 合约
例如，但您可以使用任何其他合同。将其部署到 Holesky 或 Morph。 On Morph，L1
和 L2 使用相同的 API，所以这取决于你。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

// This Greeter contract will be interacted with through the MorphMessenger across the bridge
contract Greeter {
  string public greeting = "Hello World!";

  // This function will be called by executeFunctionCrosschain on the Operator Smart Contract
  function setGreeting(string memory greeting_) public {
    greeting = greeting_;
  }
}
```

我们现在将执行`setGreeting`以跨链的方式。

### Operator Smart Contract

切换到另一条链并部署`GreeterOperator`。因此，如果您部署了`Greeter`L1 上的合约，部署`GreeterOperator`在 L2 上，反之亦然。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

// The Morph Messenger interface is the same on both L1 and L2, it allows sending cross-chain transactions
// Let's import it directly from the Morph Contracts library
import "@Morph-tech/contracts@0.1.0/libraries/IMorphMessenger.sol";

// The GreeterOperator is capable of executing the Greeter function through the bridge
contract GreeterOperator {
  // This function will execute setGreeting on the Greeter contract
  function executeFunctionCrosschain(
    address MorphMessengerAddress,
    address targetAddress,
    uint256 value,
    string memory greeting,
    uint32 gasLimit
  ) public payable {
    IMorphMessenger MorphMessenger = IMorphMessenger(MorphMessengerAddress);
    // sendMessage is able to execute any function by encoding the abi using the encodeWithSignature function
    MorphMessenger.sendMessage{ value: msg.value }(
      targetAddress,
      value,
      abi.encodeWithSignature("setGreeting(string)", greeting),
      gasLimit,
      msg.sender
    );
  }
}
```

## Calling a Cross-chain Function

我们通过执行来传递消息`executeFunctionCrosschain` and passing the following parameters:

-`MorphMessengerAddress`: This will depend on where you deployed the `GreeterOperator`合同。
- 如果您将其部署在 Holesky 上，请使用`0x50c7d3e7f7c656493D1D76aaa1a836CedfCBB16A`。如果您部署在 Morph Holesky 上，请使用`0xBa50f5340FB9F3Bd074bD638c9BE13eCB36E603d`.
-`targetAddress`: The address of the `Greeter`相对链上的合约。
-`value`: In this case, it is `0`因为`setGreeting`是不需要支付的。
-`greeting`: This is the parameter that will be sent through the message. Try passing `“This message was cross-chain!”`
-`gasLimit`:
- 如果您从 L1 向 L2 发送消息，大约`1000000`气体限制应该绰绰有余。也就是说，如果您将其设置得太高，并且`msg.value`不涵盖`gasLimit`*`baseFee`，交易将恢复。如果`msg.value`大于gas费，未使用的部分将被退还。
- 如果您要将消息从 L2 发送到 L1，请传递`0`，因为该交易将通过在 L1 上执行附加交易来完成。

### Relay the Message when sending from L2 to L1

当一笔交易从L2传递到L1​​时，必须在L1上额外发送一条“执行提现交易”。为此，您必须致电`relayMessageWithProof`关于 L1 Morph Messenger
来自 EOA 钱包的合约。

您可以直接在[Etherscan Holesky](https://Holesky.etherscan.io/address/0x50c7d3e7f7c656493d1d76aaa1a836cedfcbb16a#writeProxyContract#F3).
为此，您需要传递桥接交易和其他参数的 Merkle 包含证明。您将使用 Morph Bridge API 查询这些。

{/* TODO: finish looking into API issues */}

We're finalizing the API specifics, but for now, fetch or curl the following endpoint:

```bash
curl "https://Holesky-api-bridge.Morph.io/api/claimable?page_size=10&page=1&address=GREETER_OPERATOR_ADDRESS_ON_L2"
```

<!--
Replace `GREETER_OPERATOR_ADDRESS_ON_L2` with your GreeterOperator contract address as launched on L2. Read more about Execute Withdraw transactions
in the [Morph Messenger](/developers/l1-and-l2-bridging/the-Morph-messenger) article.
-->

:::tip
该 API 是为我们的 Bridge UI 制作的。目前尚未最终确定，未来可能会发生变化。我们将更新本指南
当 API 最终确定时。
:::

:::tip任何人都可以执行您的消息
`relayMessageWithProof`完全无需许可，因此任何愿意支付 L1 费用的人都可以代表您调用它
汽油费。此功能允许额外的支持基础设施，包括自动化此过程的工具
应用程序和用户。
:::

在 L1 和 L2 上执行并确认交易后，新的状态`greeting`于`Greeter`合同应该是`“This message was cross-chain!”`。在原始链上确认交易后，从一个链向另一个链发送消息大约需要 20 分钟。

恭喜，您现在使用我们的本机桥执行了从一条链到另一条链的交易！