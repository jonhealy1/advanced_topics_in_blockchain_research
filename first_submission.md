
#### An Introductory Analysis of Some of the Major Ideas Surrounding Blockchain Consensus  


##### Introduction  

For better or worse, the introduction of Bitcoin helped change the way that many people see and interact with the world. With the publication of the Bitcoin white paper in 2008, the notion of a blockchain was introduced and real value could be established on a digital network for the first time [1]. On a blockchain, digital assets can be created and assigned to an individual who can trust that no one else can access or spend their assets without acquiring their private keys. The author of the Bitcoin white paper - Satoshi Nakamoto - famously solved what was called the 'double-spending problem' in a network without a centralized party providing accountability. If Alice sends Bob $10 in digital tokens and tries to send Carl the same $10 in tokens only one of the transactions should count. In a blockchain there can even be one block where Bob receives the $10 from Alice and another block where Carl receives the $10 but by design only one of these blocks will be voted as valid via the longest chain rule and incorporated into the blockchain. This introduces the idea of consensus. 

The network at large must come to a consensus regarding the total state of all value in the system. To reach consensus the network must choose a node to validate a round of transactions and assemble them into a block. In Bitcoin this is done through something called 'proof-of-work'. Nodes dedicated to becoming validators compete by assembling transactions into a block so that the block that they propose is valid. To finalize this process they use computing power to hash their proposed block with a value containing a specified number of leading zeroes. If a node is successful - if other nodes in the system agree that the new block belongs on the larger blockchain - the succesful node is awarded a specified amount of currency along with any transaction costs that Users have added to their transactions for faster processing consideration. (The value created by validating blocks is also the only source of inflation in the system.)  

The publication of the Bitcoin white paper ushered in a new era for digital finance but many of the ideas that are introduced in this paper find their genesis in other work. Most people realize that Bitcoin would not be successful without previous advances in cryptography. There are other ideas as well introduced by Bitcoin that were developed elsewhere. Concerning consensus, the Hashcash paper written by Adam Back introduced the concept of proof-of-work as a means of creating security and helping to stop spam by requiring senders of email to compute cryptographic puzzles. This report will be looking at consensus as it relates to blockchains existing on public peer-to-peer networks. To achieve this we will be looking at Bitcoin then examining proof-of-work more closely by travelling back in time to look at Hashcash. From there we will travel into the future beyond Bitcoin to look at what is now the world's second most valuable blockcahin network, Ethereum. 

The two papers that will looked at in this report concerning Ethereum are the Ethereum white paper published in 2013 and the Ethereum yellow paper published later in 2014 as a more formal explanation of how the Ethereum network works. Ethereum is maybe most well known for implementing a Turing complete programming language on top of a Bitcoin like blockchain. Another important difference between Bitcoin and Ethereum is in the way block rewards are allocated with Ethereum using the GHOST protocol [6] and rewarding valid blocks that may not get implemented in the blockchain. These discarded but valid blocks are called uncle blocks and including them is thought to add security. After reviewing some of the differences between Bitcoin and Ethereum we will look at what is called proof-of-stake by examining a newer system introduced by Turing award winner and MIT professor Silvio Micali called Algorand. Proof-of-stake is important because it seeks to provide consensus in a blockchain network without expending extensive energy via electricity. Proof-of-stake generally implies that nodes with a higher stake in the system have a higher probability of being chosen to validate blocks and receive rewards for doing so. Algorand has some novel ideas about implementing proof-of-stake and this report will end by examining Algorand in greater depth.  


##### Hashcash  

Hashcash was originally proposed by Adam Back in May 1997 [7] as a means to, "throttle systematic abuse of un-metered internet resources such as email and anonymous remailers." [2] The paper, 'Hashcash - A Denial of Service Counter-Measure' was written five years later in 2002 to provide an overview of the subsequent applications, proposed improvements and results from experiments involving what is called the, 'hashcash CPU cost-function'.

Unlike other similar cost-functions known to the author at the time, hashcash is 'trapdoor-free'. A trapdoor-free cost function is defined as a cost function, where the server has no advantage in minting tokens. [2] With most cost-functions an opponent can easily create tokens, so asking for tokens to prevent things like spamming is not advantageous or beneficial for security. With hashcash and proof-of-work, only legitimate enitities would likely expend the effort needed to send messages. 

Interestingly, for the purposes of this report, one of the potential applications listed for hashcash is as a minting mechanism for the b-money electronic cash protocol famously proposed by Wei Dai [8] and generally regarded as a precursor to Bitcoin. Beck calls b-money, "an electronic cash scheme without a banking interface." [2]

##### Bitcoin  



##### References  

1. Nakamoto, Satoshi. "Bitcoin: A peer-to-peer electronic cash system." (2008).
2. Back, Adam. "Hashcash-a denial of service counter-measure." (2002).
3. Gilad, Yossi, Rotem Hemo, Silvio Micali, Georgios Vlachos, and Nickolai Zeldovich. "Algorand: Scaling byzantine agreements for cryptocurrencies." Proceedings of the 26th Symposium on Operating Systems Principles. 2017.
4. Wood, Gavin. "Ethereum: A secure decentralised generalised transaction ledger." Ethereum project yellow paper 151.2014 (2014): 1-32.
5. Buterin, Vitalik. "A next-generation smart contract and decentralized application platform." white paper 3.37 (2013).
6. Sompolinsky, Yonatan, and Aviv Zohar. "Secure high-rate transaction processing in bitcoin." International Conference on Financial Cryptography and Data Security. Springer, Berlin, Heidelberg, 2015.
7. Back, Adam. "Hashcash." (1997).
8. Wei Dai. b-money. Published at http://www.eskimo.com/ ̃weidai/bmoney.txt, Nov 1998.