#### [Q1] InSecureum balanceOf()
* (A): May be optimised by caching state variable in local variable
* (B): May be optimised by changing state mutability from view to pure
* (C): May be optimised by changing its visibility to external
* (D): None of the above

My analysis, answer, and justification: 
I don't normally see the balanceOf() function with two parameters. 
A - seems like it was just thrown on there, can't really see what it's even driving at.
B - True
C - That's not really an optimization at all, just a change in the visibility
D - False, B was true

Final: B

Actual: D - I thought Pure would be more appropriate, but it is still obvious now that its not really an "optimization" 

#### [Q2] In InSecureum, array lengths mismatch check is missing in
* (A): balanceOfBatch()
* (B): _safeBatchTransferFrom()
* (C): _mintBatch()
* (D): _burnBatch()

My analysis, answer, and justification: 
A - Present in Ln 38
B - MIA, should be confirming that all of these arrays are equal length at the start 
C - MIA, same as above
D - MIA, same as above 

Final: B, C, D

Actual: A, B, C, D -- close! I'll take it.. I thought that since line 38 made batchBalances = blah[](accounts.length); it was in the clear!

#### [Q3] The security concern(s) with InSecureum _safeTransferFrom() is/are
* (A): Incorrect visibility
* (B): Susceptibility to an integer underflow
* (C): Missing zero-address validation
* (D): None of the above

My analysis, answer, and justification:
All of the above. 
A - It should be 'Internal'
B - There should be a check for an underflow on line 93, before assigning the value to their new balance
c - This function, and its parent, are both missing the 0-addy check

Final: All of the above. A, B, & C

Actual: N/a LFG

#### [Q4] The security concern(s) with InSecureum _safeBatchTransferFrom() is/are
* (A): Missing array lengths mismatch check
* (B): Susceptibility to an integer underflow
* (C): Incorrect balance update
* (D): None of the above

My analysis, answer, and justification:
A - True, currently assumes ids.length == amounts.length
B - True, line 113 should be in a safe block
C - True, from's balances are never updated correctly

Final: A, B, C

Actual: A, C -- Honestly not sure why B isn't also true, I checked with GPT in post and it agreed... I'm clearly missing something

10/6 update: Because the solidity compiler is ^0.8+, safeMath is built in

#### [Q5] The security concern(s) with InSecureum _mintBatch() is/are
* (A): Missing array lengths mismatch check
* (B): Incorrect event emission
* (C): Allows burning of tokens
* (D): None of the above

Analysis:
A - true
B - false
C - True, no check to make sure the to address is not 0 address
D - false

Final: A, C

Actual: A B C, B's parameters are out of order, I need to pay closer attention to these things
#### [Q6] The security concern(s) with InSecureum _burn() is/are
* (A): Missing zero-address validation
* (B): Susceptibility to an integer underflow
* (C): Incorrect balance update
* (D): None of the above

Analysis:
A - 0 address validation is not needed, as this is a burn function, FALSE
B - No, based on earlier answer #Q4, I will say this is not an issue bc of the compiler V, FALSE
C - False
D - True

Final: D

Actual: N/a LFG

#### [Q7] The security concern(s) with InSecureum _doSafeTransferAcceptanceCheck() is/are
* (A): isContract check on incorrect address
* (B): Incorrect check on return value
* (C): Call to incorrect isContract implementation
* (D): None of the above

Analysis: 

Final:

Actual: B, C

#### [Q8] iThe security concern(s) with InSecureum isContract() implementation is/are
* (A): Incorrect visibility
* (B): Incorrect operator in the comparison
* (C): Unnecessary because Ethereum only has Contract accounts
* (D): None of the above

Analysis: 

Final:

Actual: B
