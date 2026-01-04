---
title: 测试框架
parent: 安全工具
nav_order: 2
---

# 测试框架

全面的测试对于安全的智能合约至关重要。

## Foundry

Foundry 是一个快速、可移植且模块化的以太坊应用开发工具包。

### 安装

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### 功能

- 快速执行
- 模糊测试支持
- Gas 优化工具
- 内置作弊码

### 示例测试

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "forge-std/Test.sol";
import "../src/MyContract.sol";

contract MyContractTest is Test {
    MyContract public contract;

    function setUp() public {
        contract = new MyContract();
    }

    function testFunction() public {
        contract.someFunction();
        assertEq(contract.value(), expectedValue);
    }
}
```

## Hardhat

Hardhat 是以太坊软件的开发环境。

### 安装

```bash
npm install --save-dev hardhat
```

### 功能

- 内置测试框架
- 网络管理
- 插件生态系统
- 调试工具

## Truffle

Truffle 是以太坊的开发框架。

### 功能

- 测试框架
- 迁移系统
- 资产管道
- 内置控制台

## 最佳实践

- 为所有函数编写测试
- 测试边界情况
- 对复杂逻辑使用模糊测试
- 测试错误条件
- 目标代码覆盖率 > 90%
