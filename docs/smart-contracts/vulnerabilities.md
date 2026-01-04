---
title: 常见漏洞
parent: 智能合约
nav_order: 1
---

# 智能合约常见漏洞

本节涵盖智能合约中发现的最常见漏洞。

## 重入攻击

重入攻击发生在合约在更新自身状态之前调用外部合约时。

### 示例

```solidity
// 易受攻击的代码
function withdraw() public {
    uint amount = balances[msg.sender];
    (bool success, ) = msg.sender.call{value: amount}("");
    require(success, "Transfer failed");
    balances[msg.sender] = 0; // 在外部调用后更新状态
}
```

### 缓解措施

- 使用检查-效果-交互模式
- 实现重入保护
- 在外部调用之前更新状态

## 整数溢出/下溢

Solidity 0.8.0+ 具有内置的溢出保护，但旧版本需要仔细处理。

### 缓解措施

- 使用 Solidity 0.8.0 或更高版本
- 对于旧版本使用 SafeMath 库
- 验证所有算术运算

## 访问控制

不当的访问控制可能允许未授权用户执行关键操作。

### 缓解措施

- 使用 OpenZeppelin 的 AccessControl
- 实现基于角色的访问控制
- 使用修饰符进行访问检查

## 抢跑攻击

交易在被打包之前会在内存池中可见，允许抢跑攻击。

### 缓解措施

- 使用提交-揭示方案
- 实现滑点保护
- 使用私有交易池
