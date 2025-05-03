#IMPERSONATOR

##Objective: 
the level is about exploiting ECDSA signature malleability to gain unauthorized access to a smart lock system. 
anyone should be able to open the lock without the need of the actual controller's private key .

##solution:
ECDSA signatures are malleable, meaning that for a given message and private key, multiple valid signatures can exist. if we have  a signature (p,q,r)
a new signature can be obtained like r` = n-r ; n being the order of the secp256k1 curve.

Access the NewLock event emitted during the deployment of the ECLocker instance and extract the original signature.

calculate new signature using the above formula.
Call the changeController function on the ECLocker contract using the new signature.
set controller to zero address and call the open function.

##keytakeaways:
ECDSA cryptography, and Ethereum's low-level operations.
