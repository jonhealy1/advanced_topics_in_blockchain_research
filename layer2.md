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