# InSecureum Race 4

#### [Q1] InSecureum implements
* (A): Atypical decimals value
* (B): Non-standard decreaseAllowance and increaseAllowance
* (C): Non-standard transfer
* (D): None of the above

My Answer and Justification: B & C

* B - IncreaseAllowance/DecreaseAllowance does not require that the sender is not the 0x0 address. 
* C - Transfer, has more arguments than standard. Usually it is just recipient and amount. _msgSender() is used instead of the sender argument. This is a vulnerability because you can transfer from Victim to Attacker that isn't involved in the tx

Actual (if diff): 
* A, B -- I don't know, I guess 8 isn't the usual value for 'decimals'.. I mean, it's not a decimal but I kind of just figured it was a placeholder. 
...
Cross-referencing on an existing contract. 
...
**AAH! On further review, decimals is usually 18, to mirror gwei. Sick. Locked in.**

#### [Q2] In InSecureum
* (A): decimals() can have pure state mutability instead of view
* (B): _burn() can have external visibility instead of internal
* (C): _mint() should have internal visibility instead of external
* (D): None of the above

My Answer and Justification: A, C

* A - correct because decimals doesn't need to read or write anything, or even calculate anything, it will just always return 8 no matter what.
* C - correct because _mint should be a protected function just like _burn()

Actual (if diff): N/a ((LFG))

#### [Q3] InSecureum transferFrom()
* (A): Is susceptible to an integer underflow
* (B): Has an incorrect allowance check
* (C): Has an optimisation indicative of unlimited approvals
* (D): None of the above

My Answer and Justification: A, B

* A - It technically is, but it is in an unchecked box, so it should be safe. 
* B - I don't know if it is incorrect per se, but there are better ways for this check to be implemented..
* Etc - I also see that in the approve function, there is no check to make sure that the tokens are being transferred from mgs.sender or someone else, to the recipient. I think this could be a vulnerability, potentially?

Actual (if diff): A, B, & C

[Q4] In InSecureum
(A): increaseAllowance is susceptible to an integer overflow
(B): decreaseAllowance is susceptible to an integer overflow
(C): decreaseAllowance does not allow reducing allowance to zero
(D): decreaseAllowance can be optimised with unchecked{}

My Answer and Justification: A, C, D

A - susceptible to overflow, because there is addition happening
C - Line 75, should be `require(currentAllowance >= subtractedValue)`
D - unsure about this one, but I know that using 'unchecked' can be a way to optimize gas..

Actual (if diff): C, D

A was incorrect because to overflow the number would have to be bigger than 2**256-1, not likely

[Q5] InSecureum _transfer()
(A): Is missing a zero-address validation
(B): Is susceptible to an integer overflow
(C): Is susceptible to an integer underflow
(D): None of the above

My Answer and Justification: C

C - the unchecked box made me think it was possible to underflow

Actual (if diff): D

D - C was wrong because with the checks and requires built into this function, underflows are not likely to happen

[Q6] InSecureum _mint()
(A): Is missing a zero-address validation
(B): Has an incorrect event emission
(C): Has an incorrect update of account balance
(D): None of the above

My Answer and Justification: A, C
Actual (if diff): ((N/a LFG))

[Q7] InSecureum _burn()
(A): Is missing a zero-address validation
(B): Has an incorrect event emission
(C): Has an incorrect update of account balance
(D): None of the above

My Answer and Justification: D

Nothing looks incorrect

Actual (if diff): B

Not really sure what's wrong with the emission event, GPT Says it should be: `emit Transfer(account, address(0), amount);`


[Q8] InSecureum _approve()
(A): Is missing a zero-address validation
(B): Has incorrect error messages
(C): Has an incorrect update of allowance
(D): None of the above

My Answer and Justification: C
Actual (if diff): B, C
