---
title: 桥
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


# Deposit from Holesky to Morph Testnet

## Instructions:

:::tip使用这里的桥

https://bridge-holesky.morphl2.io

:::

1. 打开您的 MetaMask 钱包并切换到 **Holesky** 网络。

![image1](../../assets/docs/quick-start/bridge/01.png)
![image1](../../assets/docs/quick-start/bridge/02.png)

2. 在 Morph 的 Bridge 应用程序中，单击 **连接钱包**，选择 MetaMask，并在出现提示时批准连接。

![image2](../../assets/docs/quick-start/bridge/03.png)

3. 确保在“From”下选择 **Holesky**，并在“To”下选择 Morph L2。如果没有，请点击“↓”按钮交换位置。

4. 选择您要转移的代币。

5. 单击“发送”按钮开始存款。

:::tip
如果这是您第一次转移 ERC20 代币，您需要批准 **Holesky** Bridge 合约才能访问您的 ERC20 代币。
:::

6. 会弹出一个窗口要求确认转账交易，点击**存款**。

![image3](../../assets/docs/quick-start/bridge/04.png)

7. 单击 MetaMask 中的确认按钮。转账交易完成后，代币将从您的 **Holesky** 钱包地址中扣除。

![image5](../../assets/docs/quick-start/bridge/05.png)

8. 在等待期间，您可以通过单击交易按钮来检查交易状态。

![image6](../../assets/docs/quick-start/bridge/06.png)


## How long does it take for a token to arrive to Morph Testnet ?

从 **Holesky** 到 Morph Testnet 的代币转移可能需要 8 到 14 分钟（区块在 **Holesky** 上变为安全的时间），然后才会出现在您的 Morph 钱包中。要检查您的存款交易进度，请按照以下步骤操作：

1. 单击 Bridge 网络应用程序右上角的钱包地址。

![image6](../../assets/docs/quick-start/bridge/07.png)

2. 单击“交易”。弹出面板将显示您最近的交易。

:::tip
注意：对于存款交易（L1 -> L2），一旦您的交易在 **Holesky** 上被确认为安全（8 到 14 分钟），您将看到 **成功** 状态。您的资金随后将被转发到 L2。
:::

![image8](../../assets/docs/quick-start/bridge/08.png)

3. 单击最近的 **Holesky** 交易哈希。

![image9](../../assets/docs/quick-start/bridge/09.png)

4. 您将进入浏览器中的“交易详细信息”页面。验证您的交易状态（此交易已在 **Holesky** 上确认）。

![image10](../../assets/docs/quick-start/bridge/10.png)

5. 一旦您的交易状态在 L2 上显示*成功*，请返回 Bridge 应用程序以查看您的 Morph L2 钱包中的交易哈希和资金。

![image11](../../assets/docs/quick-start/bridge/11.png)

![image12](../../assets/docs/quick-start/bridge/12.png)


# Withdraw from Morph Testnet to Holesky

To withdraw funds from Morph Testnet, follow these steps:
1. 在Morph测试网上发起提币。
2. 等待提现根在L1（**Holesky**）上发布。这通常需要几分钟，但在中断期间可能需要更长时间。
3. 证明提款。
4. 等待验证质询期，该质询期从在 L1 (**Holesky**) 上证明提款之日起持续 7 天。
5. 领取提款。

## Initiate withdrawal

1. 单击连接钱包并选择 MetaMask。如果出现提示，请在钱包中批准连接。

2. 选择提款。选择您想要提取的资产和金额。

![image13](../../assets/docs/quick-start/bridge/13.png)

3. 单击发送 ETH 至 **Holesky**。

![image14](../../assets/docs/quick-start/bridge/14.png)

4. 点击发起提现，等待几分钟确认。完成后，您需要在钱包中切换网络，然后在**Holesky**上证明提现。

![image15](../../assets/docs/quick-start/bridge/15.png)

![image16](../../assets/docs/quick-start/bridge/16.png)

5.等待批量提交完成。

![image17](../../assets/docs/quick-start/bridge/17.png)

![image18](../../assets/docs/quick-start/bridge/18.png)

## Waiting for the verification challenge period

1. 单击右上角您的地址。

2. 单击“交易”，然后单击“提款”。这将显示您最近提款及其状态的列表。或者，您可以通过单击“查看帐户”按钮（参见下图）在顶部区域找到通知。

![image19](../../assets/docs/quick-start/bridge/19.png)

![image20](../../assets/docs/quick-start/bridge/20.png)

![image21](../../assets/docs/quick-start/bridge/21.png)



3. 您可以在 Morph Explorer 上搜索交易哈希。

![image22](../../assets/docs/quick-start/bridge/22.png)

![image23](../../assets/docs/quick-start/bridge/23.png)

4. 单击 L1 State Root Submission Tx 查看交易何时写入 L1 (**Holesky**)。

![image24](../../assets/docs/quick-start/bridge/24.png)

![image25](../../assets/docs/quick-start/bridge/25.png)




## Claim the Withdrawal

1. 挑战期结束后，状态将变为“Claim”。

2. 单击“申请提款”。

![image26](../../assets/docs/quick-start/bridge/26.png)

3. 确认钱包提现。

![image27](../../assets/docs/quick-start/bridge/27.png)

4. 等待提币完成。

![image28](../../assets/docs/quick-start/bridge/28.png)

