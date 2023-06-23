### Learning with Errors Cryptography
Lua code that encrypts a message using Learning with Errors in relation to Lattice Based Cryptography. It takes a system of linear equations and shifts the values slightly by an offset to a lattice based problem. 

## 1) Generate the Private Key/ Alphabet
Take any 4 integer values, these values correspond to a solution set for some system of linear equations. This key is private information.
The Alphabet can be anything, in this program, the alphabet is the 26 letters in the english alphabet.

## 2) Generate the list of equation w/ offset
Generate a large list of linear equations and apply a random offset to its summation. This modification should make it unlikely for a non-singular partition of equations to have a solution. Then modulus this value to a large prime value to allow for modular arithmetic. 

## 3) Encode a Message
Take a partition of equations and add them together and formulate a new equation and ensure right hand side summation is still modulated to the same large prime value. This program uses a selection of 5 equations each iteration. 

Calculate the location of the character in correlation to the large prime used in the modulus. For instance, 523 can be split into 26 different parts into 20 with integer division. Take this estimate distance and multiple it to the corresponding letter number encoding. The letter "D" corresponds with 80 (4 * 20).

From the partition, take the right hand summation and add that to the location of the character and modulus by large prime. 

## 4) Decoding the Message
Using the key, plug in the private key into the equation to solve for accurate RHS summation value. 

Subtract the encoded partition summation with the accurate RHS summation value. Then solve for value by performing integer division in respect to distance calculations in encoding. 


## Why it works?
Before the offset is added in, it is possible to solve all generated equations with the private key. Additionally, the private key can solve for a combination of any partition of the equation set. An offset and distance value is generated by the by the formulas below.

### Distance = (Large Prime) // (# of Character Indexes)
### Offset < (Distance) / (# of Partitions)

The distance formula is a way to measure differing way points for each unique character. For example, splitting 13 for a 3 character alphabet would leave A in ~0, B in ~4, and C in ~8. Using this, we know the overall offset cannot be more than 4 apart or the modulus can mistake it for a different character.

This offset is selected to prevent possible overlap of similar modulus values. The addition of a randomized offset makes it impossible for a combined subset of equations to have a solution. Similarly, a user without the private key cannot know how much offset is added to each equation. This list of equations w/ offset is used as the public key. 

To encode, take a partition of equations(>2) and combine them. Add the location of the value to the right side summation result of the combined partition.

To decode, using the combined equation, calculate the actual value for the right hand side sum. Subtract this actual value from the encoded message and all that is left is the location value and the offset. Since the offset is less than 1, performing integer division will remove the offset and leave the decoded message bit. 
