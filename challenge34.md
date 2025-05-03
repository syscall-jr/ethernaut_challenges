#MAGIC ANIMAL CAROUSEL
##Objective:

call setAnimalAndSpin(animal) and immediately after the call,  getters of currentCrateId and carousel,  they must get in return of carousel(currentCrateId) the correct encoding of the animal string.

intial 10 bytes represents the animal name , the next two for the crate id , and the last 20 bytes for the owners address.

##Svulnerable function : 
encodeAnimalName() function encodes an animal name of up to 12 bytes, where the byte array intended for storing animal names is 10 bytes long.


