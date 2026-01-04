---
title: Front-Running Attacks
parent: Attack Vectors
nav_order: 2
---

# Front-Running Attacks

Front-running occurs when an attacker sees a pending transaction and submits their own transaction with higher gas to execute first.

## How Front-Running Works

1. Attacker monitors mempool for profitable transactions
2. Sees a large trade that will move price
3. Submits transaction with higher gas price
4. Attacker's transaction executes first
5. Attacker profits from price movement

## Real-World Examples

### Uniswap Front-Running

- Bots monitor large swaps
- Execute trades before the original transaction
- Profit from price impact

### NFT Minting

- Bots monitor mint transactions
- Front-run to mint rare NFTs
- Resell at higher prices

## Mitigation Strategies

### Commit-Reveal Scheme

```solidity
mapping(address => bytes32) public commitments;

function commit(bytes32 commitment) public {
    commitments[msg.sender] = commitment;
}

function reveal(uint256 value, bytes32 secret) public {
    require(keccak256(abi.encodePacked(value, secret)) == commitments[msg.sender], "Invalid commitment");
    // Execute transaction
    delete commitments[msg.sender];
}
```

### Slippage Protection

```solidity
function swap(uint256 amountIn, uint256 minAmountOut) public {
    uint256 amountOut = calculateSwap(amountIn);
    require(amountOut >= minAmountOut, "Slippage too high");
    // Execute swap
}
```

### Private Transaction Pools

- Use Flashbots for Ethereum
- Use private mempools
- Reduces front-running visibility

## MEV (Maximal Extractable Value)

Front-running is part of a broader category called MEV, which includes:
- Front-running
- Back-running
- Sandwich attacks
- Arbitrage
- Liquidations

