
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

- 


