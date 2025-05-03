#DELEGATION

##Objective :
to claim the ownership of the instance given

when the delegation contract is called with the function signature of pwn(), the fallback function forwards this call to the Delegate contract. When the Delegate's pwn() function runs via delegatecall, it sets owner = msg.sender.
However this modifies the owner variable in the Delegation contract's storage context, not the Delegate contract.

```web3.utils.keccak256("pwn()").slice(0,10)
await contract.sendTransaction({ data: "0xdd365b8b" });
```

call the Delegation contract with the calldata for pwn(),
fallback is triggered and delegatecall happens.
inside delegations's storage , the owner is changed.


