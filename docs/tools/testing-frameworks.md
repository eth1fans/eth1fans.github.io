---
title: Testing Frameworks
parent: Security Tools
nav_order: 2
---

# Testing Frameworks

Comprehensive testing is essential for secure smart contracts.

## Foundry

Foundry is a fast, portable, and modular toolkit for Ethereum application development.

### Installation

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### Features

- Fast execution
- Fuzzing support
- Gas optimization tools
- Built-in cheatcodes

### Example Test

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

Hardhat is a development environment for Ethereum software.

### Installation

```bash
npm install --save-dev hardhat
```

### Features

- Built-in testing framework
- Network management
- Plugin ecosystem
- Debugging tools

## Truffle

Truffle is a development framework for Ethereum.

### Features

- Testing framework
- Migration system
- Asset pipeline
- Built-in console

## Best Practices

- Write tests for all functions
- Test edge cases
- Use fuzzing for complex logic
- Test error conditions
- Aim for >90% code coverage

