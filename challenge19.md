#MAGICNUMBER

##Objective :  code size should be only 10 opcodes (10 bytes) and set the addess in MagicNum and return return the 32 byte magic number

##solution : 
write raw EVM bytes corresponding to contract opcodes.

intialisation opcodes: used by EVM to create the contract by replicating run time opcodes , followed by runtime opcodes: contains the execution logic of the contract.

the corresponding opcode is RETURN, which takes two arguments, location of the value in memory and the the value to be returned.
so 0x2a(42) needs to be stored in memory.
this can be done by MSTORE.
MSTORE takes in two arguments:  location of the value in stack and its size.
so push the value and size params into stack first using PUSH1 opcode.

we have to concatenate init code and runtime code , because , init code copies run time code into memory and returns it to EVM to store as the actual contract code.


