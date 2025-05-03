#DEX

##objective:
DEX or Decentralised Exchange Platform handles two types of tokens in this level , of which 10 tokens each is provided intially.
the goal is to drain all tokens either from token 1 or token 2.

formula used to exchange the token:
 no of token 2 to be returned = (amt of token 1 to be swapped * token 2 balance of  contract)/token 1 balance of  contract.

there are no floating points in solidity.whenever a division is carried out and if its  a fraction, the token amount will rounded off towards zero.

make consecutive token swaps from token 1 to token 2 and vice versa , either one of the tokens can be drained completely.

intially approve some 1000 tokens to let Dex spend using approve() function .
after approving make swap calls, such that the final balance of token 1 comes to 0.

after the 1st round, token 2 will have 110 tokens and token 1 with 90  tokens .
now swapping 20 token2 for token1 ,
(20 * 110)/90 = 24.44
24.44 is rounded off to 24.
after each consequtive swap, we are left with more tokens than previous step. 

after making the value of token2 to 65, final swap can be done which makes the value of token1 to zero. 



t


