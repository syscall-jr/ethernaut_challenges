#DENIAL

##Objective: 
to prevent the owner from withdrawing the funds when they call the withdraw() function.

#analysis: 
withdraw() function transfers one percent of the contract balance to the partner and owner.
call() method is used to send the Ether to the partner.

##solution :
setWithdrawPartner() can be called with our address so that we can become a partner.
call() function transfers all the gas value with the call unless gas value is specified. This is the vulnerability.
Also, the return values of external calls aren't checked.
Create a contract, setting it as the partner, with a fallback function that can drain all the gas.

##takeaways :
shows how a faulty contract can use a fallback function, resulting in a denial-of-service attack.
call() method in Solidity doesn't carry over errors.
