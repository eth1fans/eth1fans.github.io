---
title: Reentrancy Attacks
parent: Attack Vectors
nav_order: 1
---

# Reentrancy Attacks

Reentrancy is one of the most dangerous vulnerabilities in smart contracts.

## The DAO Attack (2016)

The most famous reentrancy attack resulted in the theft of 3.6 million ETH and led to the Ethereum hard fork.

### How It Worked

1. Attacker called `splitDAO()` function
2. Function sent ETH before updating balance
3. Attacker's fallback function called `splitDAO()` again
4. Process repeated until funds were drained

### Code Pattern

```solidity
// VULNERABLE CODE
function withdraw() public {
    uint amount = balances[msg.sender];
    msg.sender.call.value(amount)(); // External call before state update
    balances[msg.sender] = 0; // State updated too late
}
```

## Prevention

### Checks-Effects-Interactions Pattern

```solidity
function withdraw() public {
    uint amount = balances[msg.sender];
    balances[msg.sender] = 0; // Effects: Update state first
    (bool success, ) = msg.sender.call{value: amount}(""); // Interactions: External call last
    require(success, "Transfer failed");
}
```

### Reentrancy Guard

```solidity
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

contract MyContract is ReentrancyGuard {
    function withdraw() public nonReentrant {
        // Protected function
    }
}
```

## Modern Examples

- Lendf.me (2020): $25 million stolen
- BurgerSwap (2021): $7.2 million stolen
- Fei Protocol (2022): $80 million at risk

