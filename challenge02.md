#FALLBACK

##Objectives:
1. Claim ownership of the contract.
2. Reduce the balance to 0.

##Analysis:

there is a default recieve function that wll be triggered everytime someone sends ether to the smaert contract. the recieve function changes the owner of the smart contract.

to trigger the receive function, the msg value should be greater than zero and the contributions of our account message sender should be greater than zero.
 
so in the fallback function , anyone with a non-zero contribution can become the owner of the contract.

Once we claim the ownership of the contract, call the withdraw function to drain the ETH.

using foundry:

```fallbackInstance.contribute{value: 1 wei}();
address(fallbackInstance).call{value: 1 wei}("");
fallbackInstance.withdraw();

from the console:
await contract.contribute({ value: ethers.utils.parseEther("0.0001") });
```


