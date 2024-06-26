# MyToken README

## Overview

**MyToken** is an ERC-20 compliant token built on the Ethereum blockchain. It includes additional functionalities such as burning tokens and permissioned minting, and it leverages OpenZeppelin contracts for secure and efficient development.

## Features

- **ERC-20 Standard Compliance**: MyToken is fully compliant with the ERC-20 standard.
- **Mintable**: Only the owner of the contract can mint new tokens.
- **Burnable**: Users can burn their tokens to reduce the total supply.
- **Ownable**: The contract includes ownership management.
- **ERC-20 Permit**: Allows approvals to be made via signatures, reducing the number of transactions required.

## Contract Details

- **Token Name**: MyToken
- **Token Symbol**: MTK

## Dependencies

The contract uses OpenZeppelin libraries:
- `ERC20`
- `ERC20Burnable`
- `Ownable`
- `ERC20Permit`

These libraries provide a robust foundation for creating secure and functional smart contracts.

## Functions

### Constructor

```solidity
constructor() ERC20("MyToken", "MTK") ERC20Permit("MyToken") Ownable(msg.sender) {}
```
Initializes the token with the name "MyToken" and the symbol "MTK". It also sets the deployer as the owner of the contract.

### mint

```solidity
function mint(address to, uint256 amount) public onlyOwner {
    _mint(to, amount);
}
```
Mints new tokens to a specified address. This function can only be called by the owner of the contract.

### burnTokens

```solidity
function burnTokens(uint256 amount) public {
    burn(amount);
}
```
Allows users to burn a specified amount of their own tokens.

### burnTokensFrom

```solidity
function burnTokensFrom(address from, uint256 amount) public {
    burnFrom(from, amount);
}
```
Allows users to burn tokens from a specified address. The caller must have allowance for the specified amount.

### transferTokens

```solidity
function transferTokens(address to, uint256 amount) public {
    transfer(to, amount);
}
```
Allows users to transfer tokens to a specified address.

## Usage

### Deploying the Contract

To deploy the contract, use a deployment tool such as Truffle, Hardhat, or Remix. Ensure that you have the necessary dependencies installed.

### Interacting with the Contract

Once deployed, you can interact with the contract using Web3.js, Ethers.js, or any other Ethereum library. Make sure you have the contract ABI and address.

### Minting Tokens

To mint tokens, the owner can call the `mint` function:
```javascript
myTokenContract.methods.mint(receiverAddress, amount).send({ from: ownerAddress });
```

### Burning Tokens

To burn tokens, a user can call the `burnTokens` function:
```javascript
myTokenContract.methods.burnTokens(amount).send({ from: userAddress });
```

### Burning Tokens from Another Address

To burn tokens from another address, a user can call the `burnTokensFrom` function:
```javascript
myTokenContract.methods.burnTokensFrom(fromAddress, amount).send({ from: userAddress });
```

### Transferring Tokens

To transfer tokens, a user can call the `transferTokens` function:
```javascript
myTokenContract.methods.transferTokens(receiverAddress, amount).send({ from: userAddress });
```

