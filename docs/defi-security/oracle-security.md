---
title: 预言机安全
parent: DeFi 安全
nav_order: 2
---

# 预言机安全

预言机为智能合约提供外部数据。保护预言机数据对 DeFi 协议至关重要。

## 预言机风险

- **价格操纵**：攻击者操纵价格源
- **单点故障**：依赖单一预言机
- **过时数据**：使用过时的信息
- **抢跑**：利用预言机更新延迟

## 最佳实践

### 使用多个预言机

- 聚合多个来源的数据
- 使用中位数或加权平均
- 实现异常值检测

### 时间加权平均价格（TWAP）

- 减少短期操纵的影响
- 成本更高但更安全
- 适用于时间敏感度较低的操作

### 熔断机制

- 如果价格变化过快则暂停操作
- 实现最大价格变化限制
- 为关键操作添加时间延迟

## 热门预言机解决方案

- Chainlink：去中心化预言机网络
- Band Protocol：跨链预言机
- Uniswap V3 TWAP：链上价格源
- Compound Open Price Feed：社区维护

## 实现示例

```solidity
import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract PriceConsumer {
    AggregatorV3Interface internal priceFeed;
    
    constructor() {
        priceFeed = AggregatorV3Interface(0x...);
    }
    
    function getLatestPrice() public view returns (int) {
        (
            uint80 roundID,
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        require(timeStamp > 0, "Round not complete");
        return price;
    }
}
```
