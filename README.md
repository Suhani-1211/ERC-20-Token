# ERC-20-Token
# MyToken and TokenManager Contracts

## Overview

This project consists of two main Solidity smart contracts: `MyToken` and `TokenManager`. The `MyToken` contract is an ERC20 token with additional functionalities for burning and permitting, while `TokenManager` provides management capabilities for the `MyToken` contract.

### SPDX License Identifier
```solidity
// SPDX-License-Identifier: MIT
```
The project is licensed under the MIT License.

### Solidity Version
```solidity
pragma solidity ^0.8.20;
```
The contracts are written in Solidity version 0.8.20.

## Dependencies
The contracts make use of the OpenZeppelin Contracts library, version 5.0.0 or later.

## MyToken Contract

The `MyToken` contract is an ERC20 token with additional capabilities, inheriting from multiple OpenZeppelin contracts:
- `ERC20`
- `ERC20Burnable`
- `Ownable`
- `ERC20Permit`

### Contract Definition

```solidity
contract MyToken is ERC20, ERC20Burnable, Ownable, ERC20Permit {
    constructor(address initialOwner)
        ERC20("MyToken", "MTK")
        Ownable(initialOwner)
        ERC20Permit("MyToken")
    {}

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
}
```

### Features
- **ERC20 Token**: Basic ERC20 functionality.
- **Burnable**: Allows tokens to be irreversibly burned.
- **Ownable**: Ownership control, allowing for restricted access to certain functions.
- **Permit**: Provides gasless approvals using EIP-2612.

### Constructor
The constructor initializes the token with the name "MyToken" and symbol "MTK". It also sets the initial owner and initializes the permit functionality.

### Functions
- `mint(address to, uint256 amount)`: Mints new tokens to the specified address. This function can only be called by the owner.

## TokenManager Contract

The `TokenManager` contract provides management functionalities for the `MyToken` contract.

### Contract Definition

```solidity
contract TokenManager {
    MyToken public token;

    constructor(MyToken _token) {
        token = _token;
    }

    function burnTokens(uint256 amount) public {
        token.burn(amount);
    }

    function transferTokens(address to, uint256 amount) public {
        token.transfer(to, amount);
    }
}
```

### Features
- **Burn Tokens**: Allows for burning a specified amount of `MyToken`.
- **Transfer Tokens**: Allows for transferring a specified amount of `MyToken` to a given address.

### Constructor
The constructor accepts an instance of the `MyToken` contract, which it will manage.

### Functions
- `burnTokens(uint256 amount)`: Burns the specified amount of tokens.
- `transferTokens(address to, uint256 amount)`: Transfers the specified amount of tokens to the given address.

## Usage

### Deployment

1. Deploy the `MyToken` contract, providing the initial owner's address.
2. Deploy the `TokenManager` contract, providing the address of the deployed `MyToken` contract.

### Interaction

- Use the `mint` function in `MyToken` to create new tokens (owner only).
- Use the `burnTokens` function in `TokenManager` to burn tokens.
- Use the `transferTokens` function in `TokenManager` to transfer tokens.
