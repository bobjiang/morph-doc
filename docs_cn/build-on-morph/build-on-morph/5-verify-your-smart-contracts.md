---
title: 验证您的智能合约
lang: zh-CN
keywords: [morph,ethereum,rollup,layer2,validity proof,optimistic zk-rollup]
description: 使用 Morph 升级您的区块链体验 - 安全的去中心化、成本高效且高性能的乐观 zk-rollup 解决方案。现在就试试吧！
---


部署智能合约后，在我们的网站上验证您的代码至关重要[block explorer](https://explorer-holesky.morphl2.io)。这可以使用您的开发框架（例如 Hardhat）自动执行。




## Verify with development framework

大多数智能合约工具都有用于在 Etherscan 上验证合约的插件。 Blockscout 支持 Etherscan 的合约验证 API，从而可以轻松地将这些工具与 Morph 测试网一起使用。

### Verify with Hardhat

To verify your contract through hardhat, you need to add the following Etherscan and Sourcify configs to your hardhat.config.js file:

```javascript
module.exports = {
  networks: {
    morphTestnet: { ... }
  },
  etherscan: {
    apiKey: {
      morphTestnet: 'anything',
    },
    customChains: [
      {
        network: 'morphTestnet',
        chainId: 2810,
        urls: {
          apiURL: 'https://explorer-api-holesky.morphl2.io/api? ',
          browserURL: 'https://explorer-holesky.morphl2.io/',
        },
      },
    ],
  },
};
```

### Verify with Foundry

Verification with foundry requires some flags passed to the normal verification script. You can verify using the command below:

```bash
 forge verify-contract YourContractAddress Counter\
  --chain 2810 \
  --verifier-url https://explorer-api-holesky.morphl2.io/api? \
  --verifier blockscout --watch
```

## Verify with Morph explorer frontend

- 访问：[Morph block explorer](https://explorer-holesky.morphl2.io)

目前，我们支持 6 种不同的方式在我们的区块浏览器上验证您的合约。

有 2 个通用参数：

- 编译器：必须与部署时选择的一致。
- 优化：如果您没有合约优化，可以忽略。如果有，则必须与部署一致。

### Method: Solidity (Flattened Sources Code)

#### Frontend:

![fscs](../../../assets/docs/dev/contract-verify/flatsourcesol.png)

#### Flatten

压平通过[forge command](https://book.getfoundry.sh/reference/forge/forge-flatten?highlight=flatten#forge-flatten), for example:

~~~
forge flatten --输出 FlattenedL2StandardBridge.sol ./contracts/L2/L2StandardBridge.sol
~~~

### Method: Solidity (Standard JSON Input)
![sjis1](../../../assets/docs/dev/contract-verify/sjisol1.png)



#### Obtain JSON File

- 可以通过solc获取
- 可以通过remix编译器获得

![sjis2](../../../assets/docs/dev/contract-verify/sjisol3.png)

![sjis3](../../../assets/docs/dev/contract-verify/sjisol3.png)
### Method: Solidity (Multi-part files)

#### Frontend:

- 您可以根据自己的需要提交多个合同文件
![mpfs1](../../../assets/docs/dev/contract-verify/mpfsol.png)

#### SOL File Process
- 如果有导入的文件，需要修改为同级路径引用，并且这些文件必须一起提交。
![mpfs2](../../../assets/docs/dev/contract-verify/mpfsol2.png)
### Method: Vyper (Contracts)

#### Frontend:
![cv](../../../assets/docs/dev/contract-verify/cv.png)
### Method: Vyper (Standard Json Input)

#### Frontend:
![sjiv](../../../assets/docs/dev/contract-verify/sjiv.png)
### Method: Vyper (Multi-part files)

#### Frontend:
![mpfv](../../../assets/docs/dev/contract-verify/mpfv.png)

### After Verification

![avp](../../../assets/docs/dev/contract-verify/avp.png)


