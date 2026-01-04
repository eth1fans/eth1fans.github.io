---
title: Flash Loan Attacks
parent: DeFi Security
nav_order: 1
---

# Flash Loan Attacks

Flash loans allow borrowing large amounts without collateral, but can be exploited for attacks.

## What are Flash Loans?

Flash loans are uncollateralized loans that must be repaid within the same transaction.

## How Flash Loan Attacks Work

1. Attacker borrows large amount via flash loan
2. Uses funds to manipulate protocol (e.g., price oracle)
3. Executes profitable trade
4. Repays flash loan
5. Keeps profit

## Real-World Examples

- bZx protocol attacks (2020)
- Harvest Finance exploit (2020)
- Value DeFi attack (2020)

## Mitigation Strategies

### For Users

- Be aware of flash loan risks
- Monitor protocol TVL and activity
- Use protocols with flash loan protection

### For Developers

- Don't rely solely on spot prices
- Use time-weighted average prices (TWAP)
- Implement circuit breakers
- Add delays to critical operations
- Use multiple price sources

## Code Example

```solidity
// VULNERABLE: Using spot price
uint256 price = oracle.getPrice(token);

// BETTER: Using TWAP
uint256 price = oracle.getTWAP(token, 1 hours);
```

