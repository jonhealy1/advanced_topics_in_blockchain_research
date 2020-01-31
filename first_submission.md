
#### An Introductory Analysis of Some Popular Consensus Models for Public Blockchains


##### Introduction  

For better or worse, the introduction of Bitcoin helped change the way that many people see and interact with the world. With the publication of the Bitcoin white paper in 2008, the blockchain was born and real value could be established on a digital network for the first time [1]. On a blockchain, digital assets can be created and assigned to an individual who can trust that no one else can access or spend their assets without acquiring their private keys. The author of the Bitcoin white paper - Satoshi Nakamoto - famously solved what was called the 'double-spending problem' in a peer-to-peer network without a centralized party providing accountability. If Alice sends Bob $10 in digital tokens and tries to send Carl the same $10 in tokens only one of the transactions should count. In a blockchain there can even be one block where Bob receives the $10 from Alice and another block where Carl receives the $10 but by design only one of these blocks will be voted as valid via the longest chain rule and incorporated into the blockchain. The need to agree on only one final state introduces the notion of consensus.  

The network at large must come to a consensus regarding the total state of all value in the system. To reach consensus the network must choose a node to validate a round of transactions and assemble them into a block. In Bitcoin this is done through something called 'proof-of-work'. Nodes dedicated to becoming validators compete by assembling transactions into a block and making sure that the block that they propose is valid. To finalize this process they use computing power to hash their proposed block with a value containing a specified number of leading zeroes. If a node is successful - if other nodes in the system agree that the new block belongs on the larger blockchain - the succesful node is awarded a specified amount of currency along with any transaction costs that Users have added to their transactions for faster processing consideration. (The value created by validating blocks is also the only source of inflation in the system.)  

The publication of the Bitcoin white paper ushered in a new era for digital finance but many of the ideas that are introduced in this paper find their genesis in other work. Most people realize that Bitcoin would not be successful without previous advances in cryptography. There are other ideas as well, introduced to some by Bitcoin, that were developed elsewhere. Concerning consensus, the Hashcash paper written by Adam Back [2] introduced the concept of proof-of-work as a means of creating security and helping to stop spam by requiring senders of email to compute cryptographic puzzles. This report will be looking at consensus as it relates to blockchains existing on public peer-to-peer networks with a focus on the proof-of-work consensus model. To achieve this, we will be looking at the Hashcash paper and examining proof-of-work in it's original form. From there, we will continue to examine Bitcoin before jumping further into the future beyond Bitcoin to look at what is now the world's second most valuable blockcahin network, Ethereum. Ethereum introduces some important modifications to the proof-of-work model introduced by Bitcoin. 

The two papers that will be looked at in this report concerning Ethereum are the Ethereum white paper published in 2013 [5]and the Ethereum yellow paper published later in 2014 [4] as a more formal explanation of how the Ethereum network works. Ethereum is maybe most well known for implementing a Turing complete programming language on top of a Bitcoin-like blockchain. Another important difference between Bitcoin and Ethereum is in the way block rewards are allocated with Ethereum using the GHOST protocol [6] and rewarding valid blocks that may not get implemented in the blockchain. These discarded but valid blocks are called uncle blocks and including them is thought to add security.

Finally, we will briefly look at a very modern proof-of-stake solution called Algorand, which was introduced by Turing award winner and MIT professor Silvio Micali. Proof-of-stake is important because it seeks to provide consensus in a blockchain network without expending extensive energy via electricity. Proof-of-stake generally implies that nodes with a higher stake in the system have a higher probability of being chosen to validate blocks and receive rewards for doing so. Algorand has some novel ideas about implementing proof-of-stake that improve on most implementations and this report will end by examining Algorand in greater depth.   


##### Hashcash  

Hashcash was originally proposed by Adam Back in May 1997 [7] as a means to, "throttle systematic abuse of un-metered internet resources such as email and anonymous remailers" [2]. The paper, 'Hashcash - A Denial of Service Counter-Measure' was written five years later in 2002 to provide an overview of the subsequent applications, proposed improvements and results from experiments involving what is called the, 'hashcash CPU cost-function'.  

Unlike other similar cost-functions known to the author at the time, hashcash is 'trapdoor-free'. A trapdoor-free cost function is defined as a cost function, where the server has no advantage in minting tokens [2]. With most cost-functions an opponent can easily create tokens, so asking for tokens to prevent things like spamming is not advantageous or beneficial for security. With hashcash and proof-of-work, only legitimate enitities would likely expend the effort needed to send messages. 

Interestingly, for the purposes of this report, one of the potential applications listed for hashcash is as a minting mechanism for the b-money electronic cash protocol famously proposed by Wei Dai [8] and generally regarded as a precursor to Bitcoin. Beck calls b-money, "an electronic cash scheme without a banking interface" [2].   

##### Bitcoin  

The first sentence of the Bitcoin white paper sums up the author's intent quite clealy: "A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without going through a financial institution" [1]. Furthermore, Nakamoto talks about the need to prevent double-spending without a corresponding reliance on a trusted third party. There are a couple of weaknesses that are addressed concerning the trust based model [1]. 

For one, non-reversible transactions are never really possible as a central authority cannot avoid mediating dispute. This truth drives up transaction costs and also serves to limit the minimum transaction size that is feasible inside of a payment system. This idea would later develop into a cornerstone of modern blockchain conversation - the idea of micro-transactions. Super small payments to help fuel economic progress that could allow for something like a decentralized video sharing site maybe where you could send someone a fraction of a penny if you like their how-to video on spotting toucans. 

Another weakness, and this relates to the fact that transactions are potentially reversible, is that the need for trust spreads throughout the system. Nakomoto cites the need for merchants to be wary of customers. Merchants must ask for more information than what is needed. Because some fraud is unavoidable, the costs of this aggregated loss is mostly passed to consumers. As Nakomoto states, "cost and payment uncertainties can be avoided in person by using a physical currency" before pointing out that, "no mechanism exists to make payments over a communication channel without a trusted party." [1] Arguably Bitcoin has made this last statement a possibility - maybe in the future a fatal flaw will be found in the protocol and billions of dollars will go missing - and one major feature allowing for this is the concept of proof-of-work developed by Adam Back [2].

Bitcoin is based on cryptographic proof instead of trust. By assembling blocks in a chain and connecting them all with the hash of the block that came before them, Bitcoin creates a web that is computationally infeasible to reverse. To reverse any transaction, a malicious actor would have to rebuild the blockchain faster than all of the honest nodes in the system combined. There is some economic protection against this type of behaviour because any entity or group of entities with more than 51% of all network mining power would have a large stake in the system and any major breach would cause prices to plummet.

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
- Satoshi's innovation is the idea of creating a decentralized consensus protocol where nodes combine transacations into connected blocks using proof-of-work as a means of participating in the system  
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

###### Yellow paper

##### Algorand  

##### References  

[1] Nakamoto, Satoshi. "Bitcoin: A peer-to-peer electronic cash system." (2008).  

[2] Back, Adam. "Hashcash-a denial of service counter-measure." (2002).  

[3] Gilad, Yossi, Rotem Hemo, Silvio Micali, Georgios Vlachos, and Nickolai Zeldovich. "Algorand: Scaling byzantine agreements for cryptocurrencies." Proceedings of the 26th Symposium on Operating Systems Principles. 2017.  

[4] Wood, Gavin. "Ethereum: A secure decentralised generalised transaction ledger." Ethereum project yellow paper 151.2014 (2014): 1-32.  

[5] Buterin, Vitalik. "A next-generation smart contract and decentralized application platform." white paper 3.37 (2013).  

[6] Sompolinsky, Yonatan, and Aviv Zohar. "Secure high-rate transaction processing in bitcoin." International Conference on Financial Cryptography and Data Security. Springer, Berlin, Heidelberg, 2015.  

[7] Back, Adam. "Hashcash." (1997).  

[8] Wei Dai. "b-money." Published at http://www.eskimo.com/ ̃weidai/bmoney.txt, Nov 1998.    