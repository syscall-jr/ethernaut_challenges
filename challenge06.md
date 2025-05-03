#TOKEN

##Objective: the goal is to have more than 20 tokens even though we are not the owner of the contract.

In solidity version 0.6.0, there are no automatic under or over flow checks . subtraction underflowed rather than throwing an error.
also this contract doesn't use any safe guard methods.
the flaw is in the transfer function  . it only checks if the sender have sufficent balance.

Unsigned integers in Solidity cannot store negative values. If a subtraction results in a negative number, it wraps around to a huge positive value.

1.checking the balance:
```await contract.balanceOf("metamask_account")
```

2.callling the transfer function 
```await.contract.transfer("metamask_account",21)
```

[basically a  value exceeding the current balance].

3.Now there is  a massively inflated token amount due to the underflow.
await contract.transfer("0x0000000000000000000000000000000000000000", 21)



