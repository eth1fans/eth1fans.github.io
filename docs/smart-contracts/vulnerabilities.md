---
title: Common Vulnerabilities
parent: Smart Contracts
nav_order: 1
---

# Common Smart Contract Vulnerabilities

This section covers the most common vulnerabilities found in smart contracts.

## Reentrancy

Reentrancy attacks occur when a contract calls an external contract before updating its own state.

### Example

```solidity
// VULNERABLE CODE
function withdraw() public {
    uint amount = balances[msg.sender];
    (bool success, ) = msg.sender.call{value: amount}("");
    require(success, "Transfer failed");
    balances[msg.sender] = 0; // State updated after external call
}
```

### Mitigation

- Use the Checks-Effects-Interactions pattern
- Implement reentrancy guards
- Update state before external calls

## Integer Overflow/Underflow

Solidity 0.8.0+ has built-in overflow protection, but older versions require careful handling.

### Mitigation

- Use Solidity 0.8.0 or higher
- Use SafeMath library for older versions
- Validate all arithmetic operations

## Access Control

Improper access control can allow unauthorized users to perform critical operations.

### Mitigation

- Use OpenZeppelin's AccessControl
- Implement role-based access control
- Use modifiers for access checks

## Front-Running

Transactions are visible in the mempool before being mined, allowing front-running attacks.

### Mitigation

- Use commit-reveal schemes
- Implement slippage protection
- Use private transaction pools

