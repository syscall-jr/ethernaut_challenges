#HELLO ETHERNAUT

##Objective : 

interact with the contract by calling
 
await contract.info()
output:"You will find what you need in info1()." 

Instead of moving progressively through each info , info1, etc 
Inspect the ABI , and see that there is a function authenticate which takes in some passkey as input.
But there is another function called password, which retrieves a string when called.

```await contract.password()
"ethernaut0"
await contract.authenticate("ethernaut0")
Object { tx: "0x3b032b7158849a84ce97e7185cf2659a9d75fbcf4f5a1002e9a9fb6154a93360", receipt: {…}, logs: [] }
```
 
##points to note:

1.ABI gives the inteface of all the functions we can call in the instance.

2.when calling a function which changes the state (not a view function ) the wallet prompts for confirmation.


