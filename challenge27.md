#DOUBLE ENTRY POINT
##Objective : to find a bug in the CryptoVault and protect the contract from being drained of tokens. 

##analysis: 
sweepToken function is a common function used to retrieve tokens stuck in a contract.
CryptoVault operates with an underlying token that can't be swept, which is the DET token implemented  in the contract definition here.
additionally it holds 100 of legacytoken.

