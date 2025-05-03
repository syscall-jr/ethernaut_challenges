#DEX TWO

##Objective: The difference here from DEX is , we need to drain all the tokens from token1 and token2.

##analysis :
require((from == token1 && to == token2) || (from == token2 && to == token1), "Invalid tokens");
since this line from DEX is not present here, we can swap any tokens.

##solution : 
Since we can swap any token  , we can create our own ERC20 token minted by us , 
with initial supply of 400, all given to msg.sender.
intially both token1 and token2 is 10
send 100 of malicioustoken to dex two . So, that price ratio in dextwo between malicioustoken and token1 is 1:1. Same  goes for token2.


Swap 100 malicioustoken with token1. This will drain all the token1 from the Dextwo.
ask Dex to spend 300 of malicioustoken. We need this to swap 100 token1 and 200 token2. 
Swap 100 malicious with token1. This will drain all the token1 from the Dextwo.






