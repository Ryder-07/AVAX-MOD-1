# AVAX-PROOF-Module-1
# DeFi Kingdom Clone on Avalanche

Welcome to the thrilling world of blockchain-based gaming! This project is a DeFi Kingdom clone built on the Avalanche blockchain. Players can collect, build, and battle with digital assets, earning rewards through various in-game activities.

## Getting Started

### Prerequisites

- Unix Computer (MacOS or Linux) or WSL in Windows 
- Remix IDE 
- Metamask

### Setting Up Your EVM Subnet on Avalanche

1. Deploy your custom EVM subnet using the Avalanche CLI. Refer to the guide and Avalanche documentation for detailed instructions.

2. Define your native currency as an ERC20 token. This will be the in-game currency for your DeFi Kingdom clone.

3. Connect your EVM subnet to Metamask.

| **SUBNET** | **CHAIN** | **CHAINID** | **VMID**                                          | **TYPE**    |
|------------|-----------|-------------|---------------------------------------------------|-------------|
| mySubnet   | mySubnet  | 12345567    | qDN9XsRy6efv5tZw3q2ngfQzQZJyMQJEF3d3Nu4YisNi9iR4G | Subnet-EVM  |

### Deploying Smart Contracts

#### ERC20 Token Contract

```solidity
// ERC20.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ERC20 {
    string public name = "GOPALYDY";
    string public symbol = "GYD";
    // ... (contract details)
}
```
### Functions

#### 1. `transfer`

```solidity
function transfer(address recipient, uint amount) external returns (bool);
```

Transfers a specified amount of tokens from the sender's address to the recipient's address.

#### 2. `approve`

```solidity
function approve(address spender, uint amount) external returns (bool);
```

Allows the spender to withdraw a specified amount of tokens from the owner's address. Must be called before `transferFrom`.

#### 3. `transferFrom`

```solidity
function transferFrom(address sender, address recipient, uint amount) external returns (bool);
```

Transfers a specified amount of tokens from the sender's address to the recipient's address. The spender must have been approved by the owner using the `approve` function.

#### 4. `balanceOf`

```solidity
function balanceOf(address account) external view returns (uint);
```

Returns the balance of tokens held by a specific address.

#### 5. `allowance`

```solidity
function allowance(address owner, address spender) external view returns (uint);
```

Returns the remaining number of tokens that the spender is allowed to withdraw from the owner.

#### 6. `mint`

```solidity
function mint(uint amount) external;
```

Creates a specified amount of new tokens. Only callable by the contract owner.

#### 7. `burn`

```solidity
function burn(uint amount) external;
```
Compile and deploy this contract using Remix. Adjust parameters such as name, symbol, and decimals during deployment.

#### Vault Contract

```solidity
// Vault.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

interface IERC20 {
    // ... (ERC20 interface)
}

contract Vault {
    IERC20 public immutable token;
    // ... (Vault details)
}
```

Deploy the Vault contract, ensuring you provide the address of the ERC20 token contract as a parameter.

### Metamask Configuration 
```
Network name : mySubnet
New RPC URL : http://127.0.0.1:9650/ext/bc/MYp2AYrY5iZGADK17is2L9Lg34i99w3F5WVX2nccXeRwpDJ6v/rpc
Chain ID : 12345567
Currency symbol : MYSUBNET
```
### Testing Your Application

1. Use Remix to interact with the deployed smart contracts.
2. Test functions like minting, burning, depositing, and withdrawing to simulate in-game activities.
3. Confirm transactions on Metamask.

## Author 
- Gopal Yadav

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.


