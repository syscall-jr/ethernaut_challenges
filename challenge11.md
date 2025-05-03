#RE-ENTRANCY
##Objective :
steal all the funds from the contract.

##analysis: 
withdraw() function: 
 balance of the user who initiated the function call should be greater than or equal to the amount. 
it then updates the balance in mapping balances[msg.sender],, we can change this so that the function never reaches this line.

donate function :
deposit ether to the address given in the function argument.
this deposits some ether to contracts account.
create  fallback() function , so that when recieve function send ether, we can reenter the function by calling it again.
call withdraw() and supply at least the same amount as our user's donated balance to validate the if condition. 
the incoming transaction will be handled by receive() function



##takeaways:
recursively call the functions in a vulnerable smart contract, in which there are external calls, before the contract could make sensitive state changes , since it is happening after an external call .


