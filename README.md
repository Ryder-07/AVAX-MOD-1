# AVAX-PROOF-Module-1

Welcome to the AVAX-PROOF-Module-1 for the Metacrafters

## Getting Started

### Prerequisites

- Unix Computer (MacOS or Linux) or WSL in Windows 
- Remix IDE 
- Metamask

### Setting Up Your EVM Subnet on Avalanche

1. Deploy your custom EVM subnet using the Avalanche CLI. Refer to the guide and Avalanche documentation for detailed instructions.

2. Define your native currency as an ERC20 token. This will be the in-game currency for your DeFi Kingdom clone.

3. Connect your EVM subnet to Metamask.



### Deploying Smart Contracts

#### ERC20 Token Contract

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ERC20 {
    uint public totalSupply;
    mapping(address => uint) public balanceOf;
    mapping(address => mapping(address => uint)) public allowance;
    string public name = "RUDRATOKEN";
    string public symbol = "RTN";
    uint8 public decimals = 18;

    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);

    function transfer(address recipient, uint amount) external returns (bool) {
        balanceOf[msg.sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function approve(address spender, uint amount) external returns (bool) {
        allowance[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(
        address sender,
        address recipient,
        uint amount
    ) external returns (bool) {
        allowance[sender][msg.sender] -= amount;
        balanceOf[sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(sender, recipient, amount);
        return true;
    }

    function mint(uint amount) external {
        balanceOf[msg.sender] += amount;
        totalSupply += amount;
        emit Transfer(address(0), msg.sender, amount);
    }

    function burn(uint amount) external {
        balanceOf[msg.sender] -= amount;
        totalSupply -= amount;
        emit Transfer(msg.sender, address(0), amount);
    }
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

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

interface IERC20 {
    function totalSupply() external view returns (uint);
    function balanceOf(address account) external view returns (uint);
    function transfer(address recipient, uint amount) external returns (bool);
    function allowance(address owner, address spender) external view returns (uint);
    function approve(address spender, uint amount) external returns (bool);
    function transferFrom(address sender, address recipient, uint amount) external returns (bool);

    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);
}

contract Vault {
    IERC20 public immutable token;

    uint public totalSupply;
    mapping(address => uint) public balanceOf;

    constructor(address _token) {
        token = IERC20(_token);
    }

    function _mint(address _to, uint _shares) private {
        totalSupply += _shares;
        balanceOf[_to] += _shares;
    }

    function _burn(address _from, uint _shares) private {
        totalSupply -= _shares;
        balanceOf[_from] -= _shares;
    }

    function deposit(uint _amount) external {
        uint shares;
        if (totalSupply == 0) {
            shares = _amount;
        } else {
            shares = (_amount * totalSupply) / token.balanceOf(address(this));
        }

        _mint(msg.sender, shares);
        token.transferFrom(msg.sender, address(this), _amount);
    }

    function withdraw(uint _shares) external {
        uint amount = (_shares * token.balanceOf(address(this))) / totalSupply;
        _burn(msg.sender, _shares);
        token.transfer(msg.sender, amount);
    }
}

```

Deploy the Vault contract, ensuring you provide the address of the ERC20 token contract as a parameter.

### Metamask Configuration 
```
Network name : mySubnet
New RPC URL : http://127.0.0.1:9650/ext/bc/MYp2AYrY5iZGADK17is2L9Lg34i99w3F5WVX2nccXeRwpDJ6v/rpc
Chain ID : 313225
Currency symbol : RYD
```
### Testing Your Application

1. Use Remix to interact with the deployed smart contracts.
2. Test functions like minting, burning, depositing, and withdrawing to simulate in-game activities.
3. Confirm transactions on Metamask.




