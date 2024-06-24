# ERC-20-Token
# MyToken Smart Contract

## Overview

The `MyToken` contract is an ERC20-compliant token with additional functionalities such as burnable tokens, permit (gasless approvals), and ownership control. This contract uses the OpenZeppelin library for secure and tested implementation.

## Features

- **ERC20 Standard**: Implements the ERC20 standard for fungible tokens.
- **Burnable Tokens**: Tokens can be burned (destroyed), reducing the total supply.
- **Ownable**: Ownership of the contract is assigned to an address that can execute restricted functions.
- **ERC20 Permit**: Allows for gasless approvals using signatures instead of transactions.

## Requirements

- Solidity version ^0.8.20
- OpenZeppelin Contracts version ^5.0.0

## Installation

To use this contract, ensure you have the OpenZeppelin Contracts library installed in your project. You can install it via npm:

```sh
npm install @openzeppelin/contracts@5.0.2
```

## Usage

Below is an example of how to deploy and interact with the `MyToken` contract.

### Deployment

To deploy the contract, you need to provide an initial owner address. This can be done using your preferred Ethereum development environment (e.g., Hardhat, Truffle).

```solidity
const MyToken = artifacts.require("MyToken");

module.exports = async function (deployer, network, accounts) {
  const initialOwner = accounts[0];
  await deployer.deploy(MyToken, initialOwner);
};
```

### Interacting with the Contract

Once deployed, the contract exposes several functions:

- `mint(address to, uint256 amount)`: Mints new tokens to the specified address. Only the owner can call this function.
- `burn(uint256 amount)`: Burns the specified amount of tokens from the caller's account.
- Standard ERC20 functions such as `transfer`, `approve`, `transferFrom`, etc.

#### Example

```javascript
const myToken = await MyToken.deployed();

// Minting tokens
await myToken.mint("0xRecipientAddress", 1000, { from: "0xOwnerAddress" });

// Burning tokens
await myToken.burn(500, { from: "0xHolderAddress" });

// Transferring tokens
await myToken.transfer("0xAnotherAddress", 100, { from: "0xHolderAddress" });
```

## Contract Details

### Constructor

```solidity
constructor(address initialOwner)
    ERC20("MyToken", "MTK")
    Ownable(initialOwner)
    ERC20Permit("MyToken")
{}
```

The constructor initializes the token with the following parameters:
- **initialOwner**: The address that will be set as the owner of the contract.

### Functions

#### `mint`

```solidity
function mint(address to, uint256 amount) public onlyOwner {
    _mint(to, amount);
}
```

Mints new tokens to the specified address. Can only be called by the owner.
