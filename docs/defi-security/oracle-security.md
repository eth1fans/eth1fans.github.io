---
title: Oracle Security
parent: DeFi Security
nav_order: 2
---

# Oracle Security

Oracles provide external data to smart contracts. Securing oracle data is critical for DeFi protocols.

## Oracle Risks

- **Price manipulation**: Attackers manipulate price feeds
- **Single point of failure**: Relying on one oracle
- **Stale data**: Using outdated information
- **Front-running**: Exploiting oracle update delays

## Best Practices

### Use Multiple Oracles

- Aggregate data from multiple sources
- Use median or weighted average
- Implement outlier detection

### Time-Weighted Average Prices (TWAP)

- Reduces impact of short-term manipulation
- More expensive but more secure
- Suitable for less time-sensitive operations

### Circuit Breakers

- Pause operations if price changes too rapidly
- Implement maximum price change limits
- Add time delays for critical operations

## Popular Oracle Solutions

- Chainlink: Decentralized oracle network
- Band Protocol: Cross-chain oracle
- Uniswap V3 TWAP: On-chain price feeds
- Compound Open Price Feed: Community-maintained

## Implementation Example

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

