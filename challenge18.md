#RECOVERY

##Objective : 
to find the address of the deployed contract. 
call destroy()  function .

##analysis: 
the contract uses the CREATE opcode to deploy another contract.

##exploit :
get the instance address of the deployed contract.
open the address in etherscan 
look  for the internal transactions. 
The transaction flow can be seen creating another contract from the address of the first one. 
This is the address that was lost, with 0.001 Ether stored in it.

##takeaways  : 
Ether can be sent to a non-existent contract. 


