## Plasma

- Vitalik Buterin, Joseph Poon
- aug.2017 project started
- framework of secondary chains 
- communicate as little as possible with main chain
- blockchain tree - numerous smaller chains created on top of main chain
- called Plasma chains
- built with smart contracts, merkle trees
- unlimited smaller chains, copies of the parent chain
- additional chains can be created on any chain
- a plasma chain is a customizable smart contract
- allows flexibility for differet use-case scenarios
- main chain less congested - plasma chains serving different purposes and helping with load on main chain/
- communication between chains - fraud proofs - security
- root chain keeps network secure, punishes bad actors
- a plasma chain can use its own consensus algorithm 
- fraud proof exists so users can report dishonest nodes, protect their funds, and exit the transaction 
- fraud proof = file complaint
- uses MapReduce to verify data within a tree of chains in order to increase efficiency
- mass exit problem: many users exit their plasma chain at the same time and flood the root chain.
- user assets can fall back to root chain in event of a security failure on plasma chain. 
- 
- plasma mvp: transactions occur outside of ethereum
- deposits and withdrawls, entry and exit points handled on smart contract
- plasma applications: except for assets/ data going in/ out of smart contract can be handled off-chain
- state commitment: store compressed version of application cryptographically
- use merkle trees - commitments are save points for application
- 
- exiting: use commitments when leaving a plasma chain
- to withdraw money from application user proves to smart contract they have money to withdraw. This can be done with merkle proof. 
- 
- plasma 'non-custodial' sidechain 
- 1. sidechain can't steal funds
- 2. can't prevent you from claiming your funds
- accomplished by use of an almost trustless two way peg
- child chain: "trustless side chain borrowing security from its paprent chain through periodic commitments."

- 2 way peg - biggest challenge to design with minimal trust assumptions. 
- forward peg, parent -> side is easy - lock funds into a contract
- backward peg - easier to attack/manipulate side chain

- ways to resolve:
- 1. 1 way peg: no one on side chain can steal funds from parent chain. ex. Beacon chain ethereum 2.0. ETH is burned on parent chain and simultaneously minted on the PoS beacon chain as BETH
- 2. federated peg: operators control backwards peg via multisignature scheme. Operators decide when funds can be unlocked on parent chain. Side chain is effectively custoidal - federated side chains are just like centralized exchange
- 3. Plasma: allows for almost trustless 2 way peg, it does this with exit game, makes use of fraud proofs implicitly or explicitly - relies on variations of challenges that must be issued within a given timeout

- Plasma allows for increased thoughput through optimistic commtiments of many transactions on a single hash on Ethereum chain 

- with fraud proofs vs validity proofs there is trust assumption on an honest majority of block producers on parent chain. 
- in PoW a majority of miners can censor transactions - with fraud proofs if challenges are censored funds can be stolen. 
- why Plasma isn't completely trustless or completely non-custodial 


- PLASMA MVP:
- simple UTXO-based plasma chain
- enable high-throughput payment transactions
- does not support scripts or smart contracts
- 
- fraud proofs vs. validity proofs

- validity proofs: ex. zk-SNARKS - prevent incorrect state transitions from ocurring off-chain
- resource intensive
- monopolistic instead of competitive to generate so systems with validity proofs become permissioned - not decentralized
- validity proofs must be bug-free or no better than fraud proofs
- 

- fraud proofs: optimistic in nature 
- assume everything is correct until a challenge proves otherwise
- simple and cheap to generate - anyone can participate
- 

## SoK: Off the Chain Transactions  
- send transactions off-chain, blockchain only as recourse for disputes  
- "Categorizing the research into payment and state channels as well as commit-chains, we provide a comparison of protocols and properties."
- show that layer 2 can scale blockchains, secure without full collaterization, privacy of layer 2 is not granted by default, fees depend on the transmitted transaction value.
- 
- use of broadcast in blockchains limits scalability to 10 tps  
- layer two protocols are orthogonal scaling solution   
- layer 2 scale blockchains whitout changing layer 1 trust assumptions and do not introduce additional consensus mechanisms  
- off chain transactions through private communication instead of broadcasting transaction to parent chain  
- throughput shout only be bounded by bandwidth and latency between private parties
- security guaranteed through allocated collateral - in payment channel designs or with delayed transaction finality in commit-chain proposals [nocust]  
- layer 2, two properties from blockchain layer:
    - integrity: only valid transactions added to ledger
    - eventual synchronicity with an upper time-bound: valid trans eventually added, before a critical timeout
- layer 2 defined:
    - 1. do not publish every transaction to blockchain immediately
    - 2. entirely rely in consensus algorithm or parent chain 
- 2 types:  
- 1. channels are formed between n coequal parties
- 2. commit-chains rely on central but untrusted intermediary

### Channels 
- channels private peer-to-peer with pre-set rules
- 1. payment channels: off-chain payment interactions
    - rapid one-way payments, bi-directional channel designs
- 2. state channel: off-chain arbitary interactions
    - generalize payment channels to support arbitary state transitions
- channel overview: channel - n parties agree with unaminous consent to a new state of a previously agreed smart contract
- 3 phases:
    - 1. channel establishment: parties open a channel by locking collateral on blockchain. funds released by unaminous agreemnt or a pre-defined refund condition.
    - 2. transition: channel open. update channel state in 2 steps. 
        - 1. one party proposes new state transition - send signed command and state(i) to all other participants. Other parties re-compute state transition and verify proposed state before signing it and sending signature to all other parties.
    - 3. disputes: honest party does not receive n signature before local timeout, assumes disagreement about local state
- 

 




References:

[1] Gudgeon, Lewis, et al. "SoK: Off The Chain Transactions." IACR Cryptology ePrint Archive 2019 (2019): 360.
[2] Poon, Joseph, and Vitalik Buterin. "Plasma: Scalable autonomous smart contracts." White paper (2017): 1-47.
[3] Poon, Joseph, and Thaddeus Dryja. "The bitcoin lightning network: Scalable off-chain instant payments." (2016).