#HIGHER ORDER

##Objective :
to become the commander of the contract. 

##analysis: 
The contract is compiled in Solidity 0.6.12

using ABIEncoderV1,  will not perform bounds checking on function calldata, the contract does not prevent larger values from being passed in via low-level calls.

registerTreasury function is designed to accept a uint8 parameter,
inline assembly stores 32 bytes from calldata into the treasury storage slot, starting at byte offset 4 .
this can be exploited by allowing for the injection of values larger than 255.

exploit: 
                                          
