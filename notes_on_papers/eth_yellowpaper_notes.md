- written by Gavin Wood
- calls Ethereum a trustful object messaging compute framework
- Ethereum proposed by Buterin in nov. 2013
- provides some history of POW that I was unaware of *
- 

- 


12. Implementing Contracts
There are several patterns of contracts engineering that allow particular useful behaviours; two of these that I will briefly discuss are data feeds and random numbers.
12.1. Data Feeds. A data feed contract is one which pro- vides a single service: it gives access to information from the external world within Ethereum. The accuracy and timeliness of this information is not guaranteed and it is the task of a secondary contract author—the contract that utilises the data feed—to determine how much trust can be placed in any single data feed.
The general pattern involves a single contract within Ethereum which, when given a message call, replies with some timely information concerning an external phenom- enon. An example might be the local temperature of New York City. This would be implemented as a contract that returned that value of some known point in storage. Of course this point in storage must be maintained with the correct such temperature, and thus the second part of the pattern would be for an external server to run an Ethereum node, and immediately on discovery of a new block, creates a new valid transaction, sent to the contract, updating said value in storage. The contract’s code would accept such updates only from the identity contained on said server.
12.2. Random Numbers. Providing random numbers within a deterministic system is, naturally, an impossible task. However, we can approximate with pseudo-random numbers by utilising data which is generally unknowable at the time of transacting. Such data might include the block’s hash, the block’s timestamp and the block’s benefi- ciary address. In order to make it hard for malicious miner to control those values, one should use the BLOCKHASH operation in order to use hashes of the previous 256 blocks as pseudo-random numbers. For a series of such numbers, a trivial solution would be to add some constant amount and hashing the result.
13. Future Directions
The state database won’t be forced to maintain all past state trie structures into the future. It should maintain an
age for each node and eventually discard nodes that are neither recent enough nor checkpoints; checkpoints, or a set of nodes in the database that allow a particular block’s state trie to be traversed, could be used to place a maxi- mum limit on the amount of computation needed in order to retrieve any state throughout the blockchain.
Blockchain consolidation could be used in order to re- duce the amount of blocks a client would need to download to act as a full, mining, node. A compressed archive of the trie structure at given points in time (perhaps one in every 10,000th block) could be maintained by the peer network, effectively recasting the genesis block. This would reduce the amount to be downloaded to a single archive plus a hard maximum limit of blocks.
Finally, blockchain compression could perhaps be con- ducted: nodes in state trie that haven’t sent/received a transaction in some constant amount of blocks could be thrown out, reducing both Ether-leakage and the growth of the state database.
13.1. Scalability. Scalability remains an eternal con- cern. With a generalised state transition function, it be- comes difficult to partition and parallelise transactions to apply the divide-and-conquer strategy. Unaddressed, the dynamic value-range of the system remains essentially fixed and as the average transaction value increases, the less valuable of them become ignored, being economically pointless to include in the main ledger. However, several strategies exist that may potentially be exploited to pro- vide a considerably more scalable protocol.
Some form of hierarchical structure, achieved by ei- ther consolidating smaller lighter-weight chains into the main block or building the main block through the in- cremental combination and adhesion (through proof-of- work) of smaller transaction sets may allow parallelisa- tion of transaction combination and block-building. Par- allelism could also come from a prioritised set of parallel blockchains, consolidated each block and with duplicate or invalid transactions thrown out accordingly.
Finally, verifiable computation, if made generally avail- able and efficient enough, may provide a route to allow the proof-of-work to be the verification of final state.