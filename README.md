## A simple smart contract using solidity for a token transfer system.

## Requirements:
- 1.Ganache
- 2.Truffle
- 3.Node.js

## Deployment Steps:
- 1.Install truffle
  ``` 
   npm install -g truffle
   ```
- 2.Create project folders and initialize
 ``` 
   mkdir simple-token
 cd simple-token
truffle init
   ```
- 3.Install Ganache

- 4.Create a file in contracts/SimpleToken.sol
 ``` 
   // SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleToken {
    string public name = "SimpleToken";
    string public symbol = "SIM";
    uint8 public decimals = 18;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;
    event Transfer(address indexed from, address indexed to, uint256 value);

    constructor(uint256 initialSupply) {
        totalSupply = initialSupply * (10 ** uint256(decimals));
        balanceOf[msg.sender] = totalSupply;
    }

    function transfer(address to, uint256 value) public returns (bool success) {
        require(to != address(0), "Invalid recipient");
        require(balanceOf[msg.sender] >= value, "Insufficient balance");

        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        emit Transfer(msg.sender, to, value);
        return true;
    }
}
```
- 5.Create file in migrations/2_deploy_tokens.js
```
const SimpleToken = artifacts.require("SimpleToken");

module.exports = function (deployer) {
  deployer.deploy(SimpleToken, 1000); 
};
 ```
6.Configure Ganache in truffle-config.js
```
module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",     // Ganache's RPC server
      port: 7545,            // Ganache GUI default port
      network_id: "*",       // Match any network
    },
  },
  compilers: {
    solc: {
      version: "0.8.0",      // Match contract compiler version
    }
  }
};
 ```
7.Compile 
 ``` 
   truffle compile 
   ```
- 8.Make sure that Ganache is Running
- 9.Deploy
 ``` 
   truffle migrate
   ```

## Deployment Output:
![Image](https://github.com/user-attachments/assets/b05f7ef1-6937-4e92-baf4-cddc1e2ecf00)

![Image](https://github.com/user-attachments/assets/fda02e34-d9a4-4d9b-99ee-b7098ef69d93)
