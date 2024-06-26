# Chandigarh University Summer Internship With Metacrafters Project 03 

## Introduction 

For this project, you will write a smart contract to create your own ERC20 token and deploy it using HardHat or Remix. Once deployed, you should be able to interact with it for your walk-through video. From your chosen tool, the contract owner should be able to mint tokens to a provided address and any user should be able to burn and transfer tokens.

The **"ERC20_self"** contract is an ERC20-compliant smart contract representing a custom token on the Ethereum blockchain. It includes essential attributes such as the token's name, symbol, decimals, total supply, and individual balance tracking for addresses. The contract's functions allow token transfers between addresses, approval of spending limits, and the ability for the contract owner to mint new tokens. The contract also supports token burning, enabling any address to destroy a specified amount of its own tokens. Access controls, such as the "onlyOwner" modifier, ensure that certain functions can only be called by the contract's owner, providing necessary security measures. The contract facilitates essential token management functionalities while adhering to the ERC20 standard.

![image](https://github.com/Metacrafters0x1/Eth-Avax_Intermediate_Project_02/assets/149813536/7c02df2d-36f8-478f-be0e-9dd83ee380b4)


## Contract Explanation 

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract Custom_ERC20 is ERC20 {

    constructor(string memory _Token_Name, string memory _Token_Symbol, uint256 initialSupply) ERC20(_Token_Name, _Token_Symbol) {
        _mint(msg.sender, initialSupply);
    }

    function mint(address _to, uint256 _amount) public {
        _mint(_to, _amount);
    }

    function burn(uint256 _amount) public {
        _burn(msg.sender, _amount);
    }

    // Custom transfer function
    function customTransfer(address _to, uint256 _amount) public returns (bool) {
        require(_to != address(0),"Invalid Recevier Address");
        
        // Call the inherited transfer function
        _transfer(msg.sender, _to, _amount);
        return true;
    }
}
```

1. The provided Solidity smart contract represents a custom ERC20 token named **Custom_ERC20."** This contract is designed to adhere to the ERC20 standard, which is a widely used Ethereum token standard, ensuring compatibility with various platforms and applications. The contract includes essential attributes, such as the token's name, symbol, and decimal places, which define the token's divisibility. The "totalSupply" variable represents the overall number of tokens in circulation, and the "balanceOf" mapping tracks the token balances for each address. The "allowance" mapping allows addresses to approve others to spend a certain amount of tokens on their behalf, a common feature in token systems. The contract employs an "owner" variable, granting special privileges to the creator of the contract, as indicated by the "onlyOwner" modifier. This ownership control ensures that crucial functions, like token minting and other administrative actions, can only be executed by the contract owner, enhancing security and control.

2. The contract also defines events, including the **"Transfer"** and **"Approval"** events. The **"Transfer"** event is emitted whenever tokens are moved from one address to another, serving as an essential mechanism for tracking token movements and enabling external systems to monitor transactions. The **"Approval"** event is emitted when an address approves another address to spend tokens on its behalf, which is often used for decentralized applications requiring permission-based interactions.

3. The contract features functions essential for token management. The **"transfer"** function enables the direct transfer of tokens from the sender's address to another address, provided the sender has a sufficient balance. The "approve" function permits the sender to approve a certain address (spender) to spend a specified amount of tokens on its behalf, which is essential for allowing controlled token transfers by third parties. The **"transferFrom"** function allows a designated spender to move tokens from one address to another, but only if the owner has given prior approval for this action.

4. The **"mint"** function is reserved for the contract owner, allowing them to create and issue new tokens, thereby increasing the total supply. Conversely, the **"burn"** function permits any address to destroy (burn) a specified amount of its own tokens, reducing the overall supply.

5. This contract aims to provide a comprehensive ERC20 token management solution, encompassing essential features such as transfers, allowances, minting, and burning. The inclusion of an ownership mechanism ensures that critical functions are securely controlled by the contract creator. By adhering to the ERC20 standard and providing these features, this contract serves as a fundamental building block for various decentralized applications, financial systems, and token-based platforms operating within the Ethereum ecosystem.

