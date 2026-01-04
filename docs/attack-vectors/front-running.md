---
title: 抢跑攻击
parent: 攻击向量
nav_order: 2
---

# 抢跑攻击

抢跑发生在攻击者看到待处理的交易并提交自己的交易，使用更高的 gas 价格以首先执行。

## 抢跑如何工作

1. 攻击者监控内存池以寻找有利可图的交易
2. 看到将影响价格的大额交易
3. 提交具有更高 gas 价格的交易
4. 攻击者的交易首先执行
5. 攻击者从价格变动中获利

## 真实案例

### Uniswap 抢跑

- 机器人监控大额交换
- 在原始交易之前执行交易
- 从价格影响中获利

### NFT 铸造

- 机器人监控铸造交易
- 抢跑以铸造稀有 NFT
- 以更高价格转售

## 缓解策略

### 提交-揭示方案

```solidity
mapping(address => bytes32) public commitments;

function commit(bytes32 commitment) public {
    commitments[msg.sender] = commitment;
}

function reveal(uint256 value, bytes32 secret) public {
    require(keccak256(abi.encodePacked(value, secret)) == commitments[msg.sender], "Invalid commitment");
    // 执行交易
    delete commitments[msg.sender];
}
```

### 滑点保护

```solidity
function swap(uint256 amountIn, uint256 minAmountOut) public {
    uint256 amountOut = calculateSwap(amountIn);
    require(amountOut >= minAmountOut, "Slippage too high");
    // 执行交换
}
```

### 私有交易池

- 以太坊使用 Flashbots
- 使用私有内存池
- 减少抢跑可见性

## MEV（最大可提取价值）

抢跑是更广泛类别 MEV 的一部分，包括：
- 抢跑
- 后跑
- 三明治攻击
- 套利
- 清算
