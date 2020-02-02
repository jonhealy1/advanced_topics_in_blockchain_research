
#### Eth White Paper Notes

##### Ethereum  

- Ethereum does not use the UTXO model like Bitcoin, it uses the account/balance model that is supposed to be better for smart contracts
- account balance model can provide incremental updates to states while the UTXO model can only provide full outputs
- "This makes a significant savings of transaction size for applications like non-fungible
tokens (e.g., Ethereum’s ERC-721 token), in which the
state is a set of unique identifiers."
  
###### White paper  

Introduction/ History  

- Ethereum was first introduced to the world via Vitalik Buterin in the Ethereum white paper [5]  
- Ethereum intends, "to provide a blockchain with a built-in fully fledged Turing-complete programming language that can be used to create 'contracts' that can be used to encode arbitrary state transition functions."
- Bitcoin allowed for some programming funtionality which led to various proposals like colored coins and namecoin for domain names (explain more)
- Vitalik champions the DAO or digital autonomous organization. The assets and bylaws of an entire organization are all written in smart contracts and stored on a blockchain
- research: e-cash proposals of the 1980s and 1990s
- research: Hal Finney 2005 introduces a concept of 'reusable proofs of work'. Uses hashcash and b-money but fails because it relies on trusted computing on the backend
- consensus protocols, like byzantine fault tolerant assumed a network of known participants but in an anomynous setting a network is vulnerable to sybil attacks - a node can create many other nodes to secure a majority share
- Satoshi's innovation is the idea of creating a decentralized consensus protocol where nodes combine transacations into connected blocks using proof-of-work as a means of participating in the system.  

State Transition System    

- Bitcoin can be thought of as a 'state transition system'  
- A state consists of the ownership status of all bitcoins  
- The transition function takes a state and a transaction and outputs a new state
- Coins in Bitcoin are technically 'unspent transaction outputs' or UTXO
- each UTXO has a denomination and an owner defined by a 20 byte address which is the public key. 
- A transaction has one or more inputs - each input contains a, "reference to an existing UTXO and a cryptographic signature produced by the private key associated with the owner's address, and one or more outputs, with each output containing a new UTXO to be added to the state."

Mining   

- each transaction in the block must provide a state transition that is valid
- SHA256 of every block as a 256 bit number must be less than a dynamically adjusted target ex. 2^190 when this paper was written
- SHA256 is designed to pseudorandom and the only way to find a hash that meets the above criteria is through trial and error
- To do this the nonce is incremented and then the entire block is hashed again.
- At target of 2192 this means an average of 264 tries. Target is recalibrated every 2016 blocks so that a new block is produced every 10 minutes.
- Attacks will focus on the one part of the system not protected by cryptography - the order of transactions
- Vitalik outlines this attack: 
    1. Send 100 BTC to merchant 
    2. wait for product
    3. Produce another transacation sending the 100 BTC to himself
    4. Convince network his transaction came first
- To make this work attacker would have to redo the blockchain form the point at which the merchant accepted the 100 BTC and sent the product - the attacker would have to rebuild the chain beyond where it had advanced to needing more than 51% of all mining power

Merkle Trees  

- important to Bitcoin and other blockchain protocols
- scalability - each block is stored in a multi-level data structure
- the hash of a block is only a hash of the block header
- block header is roughly 200 bytes and contains the timestamp, nonce, previous block hash and the root hash of a data structure which is a merkle tree storing all the transactions in any block
- A merkle tree is a type of binary tree
- leaf nodes contain the underlying data
- intermediate nodes where each node is the hash of it's two childern
- finally a single root node also the hash of its two children which is called the Merkle root
- the merkle tree allows data in a block to be queried efficiently. a node needs only the header of a block and the small part of the tree relevant to them to check their data to know it is correct
- hashes propogate up, a fake transaction in a leaf node will cause the root hash to be invalid.
- a full node on the network takes up about 15 GB. of disk space as of April 2014 growing by over 1GB per month. 
- SPV or simplified payment verification is a system that allows for light nodes to exist
- light nodes only need to download block headers, verify the Proof-of-work on the block headers and then download branches of the merkle tree that are relevant
- this is used to determine whether relevant transactions have occurred

Alternative Applications  

- Nick Szabo 2005 concept of "secure property titles with owner authority" describing a system that could be someday implemented with "new advances in replicated database technology" - these advances did not exist yet - never implemented
- After 2009 with Bitcoin, new ideas emerged:
    1. Namecoin: 2010 - decentralized name registration database\
    - in decentralized protocols like Bitcoin or Tor there is a need to identify accounts beyond the use of a public key hash
    - uses first to file which works with consensus on Bitcoin
    2. Colored coins: people can creat their own tokens on top of Bitcoin
    - a person can create a new currency by assigning a color to a specific UTXO. The protocol defines the color of other UTXO to be the same as the color of the inputs that the transaction creating them spent - through recursion. 
    - A User can have a wallet with UTXO of only a specific color
    3. Metacoins: protocol on top of Bitcoin. Bitcoin transactions store Metacoin transactions with a a different state transaction function - Vitalik calls this APPLY
    - mining, networking handled by Bitcoin
    - ?? not sure how this works

- Approaches that build on top of Bitcoin - as opposed to building brand new blockchains - does not inherit SPV
- SPV works - it uses blockchain depth - it's safe to say a transaction is valid because it happened a while ago
- meta protocols cannot force the blockchain not to include transactions that are not valid 'within the context of their own protocols'
- a fully secure SPV meta protocol would have scan the entire blockchain to determine if transactions are valid
- Vitalik says that all bitcoin-based meta protocols rely on a trusted server to provide data - goes against a primary purpose - eliminate the need for trust.   

Scripting  

- Bitcoin allows for a 'weak version' of smart contracts
- UTXO can be owned by a public key and also by more "complicated script expressed in a simple stack based programming language"
- spending a UTXO, a transaction provides data that satisfies script
- basic public key ownership mechanism is employed with a script
- script takes elliptic curve signature as input, verifies it against a transaction and the address that owns the UTXO returning 1 if the verification is successful and 0 otherwise. 
- more complicated scripts exist - a script can be creares that depends on signatures from 2 out of 3 public keys to validate ("multisig")  

- Scripting has limitations:
1. Not Turing complete: missing loops - done to avoid infinite loops during transaction verification - can be programmed but code becomes very long. 
- Vitalik talks about an alternative elliptic curve signature that would require 256 repeated rounds of mulitplication
2. Value-blindness: UTXO script can not provide fine grained control over amounts
3. Lack of state: UTXO can either be spent or unspent - can not be used for multi-stage contracts or scripts which keep any other internal state
- hard to implement multi-stage option contracts, decentralized exchange offers, or two stage cryptographic commitment protocols (for secure computational bounties)
- UTXO can only be used to build simple one off contracts and not stateful contracts such as DAO - makes meta protocols difficult to implement - binary state with value blindness means that implementing withdrawl limits is also impossible  

Creating a new blockchain is diffcult. Scripting is limited, meta protocols suffer from faults in scalability, ethereum intends to build a generalized framework that allows for these things

Ethereum  

- merge and improve concepts of scripting, altcoins, and on chain meta protocols
- 'allow developers to create arbitrary consensus-based applications that have the scalability, standardization, feature-completeness, ease of development and interoperability offered by these three paradigms all at the same time.'
- build turing complete language which adds massive amounts of potential

Ethereum accounts

- a state is made up of objects called 'accounts' 
- contains 4 fields:
    1. nonce: counter to make sure each transaction can only be processed once
    2. ether balance of account
    3. account's contract code, if it exists
    4. account's storage, default = empty
- Ether is the crypto fuel - used to pay transaction fees
- 2 types of accounts:
    1. externally owned accounts: controlled by private keys
    2. contract accounts: controlled by their contract code
- externally owned account has no code and someone can send messages from an externally owned account by creating and signing a transaction
- in contract account - everytime the contract account receives a message its code activates - "this allows it to read and write to internal storage and send other message or create contracts in turn."  

Message and Transactions  

- message are like transactions in Bitcion - 3 differences
    1. eth message can be created by external entity (like Bitcoin) or contract
    2. explicit option in eth for messages to contain data
    3. of recipient of message os contract account can return response - this means eth messages can act as functions
- transaction: signed data package that stores a message to be sent from an externally owned account
- trans contains recipient of message, signature identifying sender, amount oether and the data to send, as well as two values - STARTGAS and GASPRICE
- to prevent infinite loop and exponential blowups - set limit to how many steps of code can execute including initial message and additional message created during execution
- STARTGAS = limit, GASPRICE = fee to pay miner per computational step
- if transaction execution runs out of gas all state changes revert - except for the payment of fees, if transactoin execution halts with gas remaining it is refunded to sender. 
- there is a separate transaction type and message type for creating contract - address of contract is calculated based on hash of the account nonce and transaction data. 
- first class citizen property - contracts have equivalent powers to external accounts - send message and create other contracts
- address of contract is calculated based on hash of account nonce and trans data  

Code Execution  

- code is written in low level, stack based bytecode languag called EVM code
- code consists of a series of bytes - each byte represents an operation
- code execution is an infinite loop repeatedly performing an operation at the current program counter (which begins at zero) then incrementing the program counter by one until the code ends or an error or STOP or RETURN instruction is detected.
- Operations can store data in 3 places:
    - stack: last in first out container to which 32 byte values can be pushed or popped
    - memory: infintiely expandable byte array
    - long-term storage: key/value store where keys and values ar bothe 32 bytes. Storage persists for the long term ulike stack and memory.
- also, code can access the value, senderm and data of incoming message as well as block header data 
- code can return a byte array of data as output
- full computational state of EVM defined by tuple = (block_state, transaction, message, code, memory, stack, pc, gas)
- block_state is the global state containing all aacounts and includes balances and storage
- every round of execution the current instruction is found by taking the pc-th byte of code and each instruction has its own definition relating to how it affects the tuple
- ADD pops two items off the stack and pushes their sum, reduces gas by 1 and increments pc by 1
- SSTORE pushes the top two items off the stack and inserts the second item into the contract's storage at the index specified by the first item as well as reducing gas by up to 200 and incrementing pc by 1
- Vitalik says a basic implementation of ethereum can be done in a few hundreds line of code

Blockchain and mining  

- unlike Bitcoin, Eth blocks contain a copy of both the transaction list and the most recent state. Two other values, the block number and the difficulty are also stored in the block
- block validation algorithm eth:
1. check previous block referenced valid
2. check timestamp of block is greater than previous block and not more than 15 minutes into the future
3. check block number, difficulty, transaction root, uncle root, and gas limit
4. check proof of work
5. let s[0] be the STATE_ROOT of the prev block
6. let TX be the transaction list with n transactions. for all n setS[i+1] = APPLY(S[i],TX[i]). If any application returns an error or if the total gas consumed in the block up until this point exceeds the GASLIMIT return an error
7. let S_FINAL be S[n] but adding the block reward paid to the miner
8. check if S_FINAL is the same as the STATE_ROOT - if it is block is valid

- seems inefficient because it stores the entire state with each block
- should be just as efficient as Bitcoin because the state is stored in a tree structure and after every block only a small part of the tree needs to be changed.
- in general between two blocks most of the tree should be the same so data can be stored once and referenced twice using pointers (ie hash of subtree)
- A 'Patricia tree' is used, a modification to a merkle tree that allows for nodes to be inserted and deleted efficiently
- because of all state info is part of the last block there is no need to store entire blockchain history
- Vitalik says if this was applied to Bitcoin it could provide a 5-20x savings in space

Modified GHOST implementation  

- GHOST 'greediest heaviest observed subtree' introduced by Sompolinsky and Zohar in 2-13
- blockchains with fast confirmation times suffer from reduced security because of a high stale rate
- blocks take time to propogate through the network
- miner A mines block, miner B mines another block before miner A's block reaches B, miner B's block will be wasted and will not be contributing to the overall network security
- Centralization issue:
    - if miner A is a mining pool with 30% hashpower and B has 10% hashpower
    - A will have risk of producing stale block 70% of time while B will be 90%
    - if block interval is short enough to have high stale rate, A will be much more efficient because of size.
    - "blockchains which produce blocks quickly are likely to lead to one mining pool having a large enough percentage of the network hashpower to have de facto control over the mining process."
- GHOST solves network security by including stale blocks in calculating which chain is the longest, stale children of block's ancestors (uncles) are added to the calculation for longest chain
- centralization: buterin goes beyond GHOST and allows stales to be regustered in main chain so mining awards block reward
- stale block receives 93.75% of base reward and nephew that includes stale block receives remaining 6.25%. trans fees are not awarded to uncles
- eth uses simple version of GHOST that only goes down 5 levels
- stale block can only be included as uncle by 2nd to 5th generation child of its parent - not any block with more distant relation
- unlimited GHOST too complicated 
- unlimited GHOST with compensaton used in eth removes the incentive for miner to mine on main chain and not the chain of a public attacker
- calculations show that five-level GHOST with incentives is over 95% efficient even with a 15s block time and miners with 25% hashpower show chentralization gains of less than 3%

Fees  

Computation and Turing Completeness  

- EVM allows jumping in two ways:
1. JUMP instruction so that program can jump back 
    - JUMPI for conditional jumping ex. while x<27 : x = x*2
2. Contracts call other contracts which can allow for looping via recursion
    - problem: can mailicious users shut miners and full nodes done by forcing them to enter an infinite loop
    - arises because of halting problem - no way to tell if any program will ever halt
    - solved by requiring transaction to set a max num of computation steps - if execution takes longer computation is reverted but fees are still paid
- ALternative to turing complete is turing incomplete where JUMP and JUMPI do not exist - only one copy of each contract is allowed to exist in the call stack at any given time.

Mining  

- eth uses a mining algo based on randomly generating a unique hash functoin for every 1000 nonces to remove the potential for specialized mining hardware to take over the network
- design mining algo so that mining requires access to entire blockchain - so they can verify each transaction - removes need for centralized mining pools where they provide block headers for miners
- helps increase the number of full nodes so the network remains decentralized if most users prefer light clients

Scalability  
- like Bitcoin every trans needs to processed by every node in the network 
- btc blockchain is about 20gb growing by 1mb per hour
- eth will be worse because there will be applications build on top of the protocol
- it will be helped because eth store state not fill history
- risks: if blockcahin gets too big only a few large businesses would run full nodes
- 













