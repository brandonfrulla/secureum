#### [Q1] The security concern(s) with InSecureumLand is/are
* (A): Single-step ownership change
* (B): Incorrectly implemented KYC check using Merkle proofs
* (C): Missing time-delayed change of critical parameters
* (D): Accidentally sent Ether gets locked in contract

My Answer & Justification:

[Answers (if different)]:

[Q2] The security concern(s) with InSecureumLand setOperator() is/are
(A): Missing zero-address validation
(B): Missing event emission
(C): Incorrect modifier
(D): None of the above

My Answer & Justification:

[Answers (if different)]:

[Q3] The security concern(s) with InSecureumLand mintLands() is/are
(A): Minting could exceed max supply
(B): Minting could exceed maxMintPerTx
(C): Minting could exceed maxMintPerAddress
(D): None of the above

My Answer & Justification:

[Answers (if different)]: 

[Q4] Missing threshold check(s) on parameter(s) is/are a concern in

(A): mintLands
(B): startPublicSale
(C): contributorsClaimLand
(D): None of the above

My Answer & Justification:

[Answers (if different)]: 

[Q5] The security concern(s) with InSecureumLand contributors claim functions is/are

(A): Anyone can call startContributorsClaimPeriod
(B): Anyone can call stopContributorsClaimPeriod
(C): Anyone can call contributorsClaimLand
(D): None of the above

My Answer & Justification:

[Answers (if different)]: 

[Q6] The security concern(s) with InSecureumLand random number usage is/are

(A): It depends on miner-influenceable block.timestamp
(B): It depends on miner-influenceable blockhash
(C): It depends on deprecated Chainlink VRF v1
(D): None of the above

My Answer & Justification:

[Answers (if different)]: 

[Q7] The documentation/readability concern(s) with InSecureumLand is/are

(A): Stale comments
(B): Missing NatSpec
(C): Minimal inlined comments
(D): None of the above

My Answer & Justification:

[Answers (if different)]: 

[Q8] Potential gas optimization(s) (after appropriate security considerations) in InSecureumLand is/are

(A): Removing nonReentrant modifier if mint addresses are known to be EOA
(B): Using _mint instead of _safeMint if mint addresses are known to be EOA
(C): Using unchecked in for loop increments
(D): None of the above

My Answer & Justification:

[Answers (if different)]: 