---
title: 重入攻击
parent: 攻击向量
nav_order: 1
---

# 重入攻击

重入是智能合约中最危险的漏洞之一。

## DAO 攻击（2016）

最著名的重入攻击导致 360 万 ETH 被盗，并导致以太坊硬分叉。

### 工作原理

1. 攻击者调用 `splitDAO()` 函数
2. 函数在更新余额之前发送 ETH
3. 攻击者的回退函数再次调用 `splitDAO()`
4. 重复此过程直到资金被耗尽

### 代码模式

```solidity
// 易受攻击的代码
function withdraw() public {
    uint amount = balances[msg.sender];
    msg.sender.call.value(amount)(); // 在状态更新之前的外部调用
    balances[msg.sender] = 0; // 状态更新太晚
}
```

## 预防

### 检查-效果-交互模式

```solidity
function withdraw() public {
    uint amount = balances[msg.sender];
    balances[msg.sender] = 0; // 效果：首先更新状态
    (bool success, ) = msg.sender.call{value: amount}(""); // 交互：最后进行外部调用
    require(success, "Transfer failed");
}
```

### 重入保护

```solidity
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

contract MyContract is ReentrancyGuard {
    function withdraw() public nonReentrant {
        // 受保护的函数
    }
}
```

## 现代案例

- Lendf.me（2020）：被盗 2500 万美元
- BurgerSwap（2021）：被盗 720 万美元
- Fei Protocol（2022）：8000 万美元面临风险
