
#### An Introductory Analysis of Some Popular Consensus Models for Public Blockchains


##### Introduction  

For better or worse, the introduction of Bitcoin helped change the way that many people see and interact with the world. With the publication of the Bitcoin white paper in 2008, the blockchain was born and real value could be established on a digital network for the first time [1]. On a blockchain, digital assets can be created and assigned to an individual who can trust that no one else can access or spend their assets without acquiring their private keys. The author of the Bitcoin white paper - Satoshi Nakamoto - famously solved what was called the 'double-spending problem' in a peer-to-peer network without a centralized party providing accountability. If Alice sends Bob $10 in digital tokens and tries to send Carl the same $10 in tokens only one of the transactions should count. In a blockchain there can even be one block where Bob receives the $10 from Alice and another block where Carl receives the $10 but by design only one of these blocks will be voted as valid via the longest chain rule and incorporated into the blockchain. The need to agree on only one final state introduces the notion of consensus.  

The network at large must come to a consensus regarding the total state of all value in the system. To reach consensus the network must choose a node to validate a round of transactions and assemble them into a block. In Bitcoin this is done through something called 'proof-of-work'. Nodes dedicated to becoming validators compete by assembling transactions into a block and making sure that the block that they propose is valid. To finalize this process they use computing power to hash their proposed block with a value containing a specified number of leading zeroes. If a node is successful - if other nodes in the system agree that the new block belongs on the larger blockchain - the succesful node is awarded a specified amount of currency along with any transaction costs that Users have added to their transactions for faster processing consideration. (The value created by validating blocks is also the only source of inflation in the system.)  

The publication of the Bitcoin white paper ushered in a new era for digital finance but many of the ideas that are introduced in this paper find their genesis in other work. Most people realize that Bitcoin would not be successful without previous advances in cryptography. There are other ideas as well, introduced to some by Bitcoin, that were developed elsewhere. Concerning consensus, the Hashcash paper written by Adam Back [2] introduced the concept of proof-of-work as a means of creating security and helping to stop spam by requiring senders of email to compute cryptographic puzzles. This report will be looking at consensus as it relates to blockchains existing on public peer-to-peer networks with a focus on the proof-of-work consensus model. To achieve this, we will be looking at the Hashcash paper and examining proof-of-work in it's original form. From there, we will continue to examine Bitcoin before jumping further into the future beyond Bitcoin to look at what is now the world's second most valuable blockcahin network, Ethereum. Ethereum introduces some important modifications to the proof-of-work model introduced by Bitcoin. 

The two papers that will be looked at in this report concerning Ethereum are the Ethereum white paper published in 2013 [5]and the Ethereum yellow paper published later in 2014 [4] as a more formal explanation of how the Ethereum network works. Ethereum is maybe most well known for implementing a Turing complete programming language on top of a Bitcoin-like blockchain. Another important difference between Bitcoin and Ethereum is in the way block rewards are allocated with Ethereum using the GHOST protocol [6] and rewarding valid blocks that may not get implemented in the blockchain. These discarded but valid blocks are called uncle blocks and including them is thought to add security.

Finally, we will briefly look at a very modern proof-of-stake solution called Algorand, which was introduced by Turing award winner and MIT professor Silvio Micali. Proof-of-stake is important because it seeks to provide consensus in a blockchain network without expending extensive energy via electricity. Proof-of-stake generally implies that nodes with a higher stake in the system have a higher probability of being chosen to validate blocks and receive rewards for doing so. Algorand has some novel ideas about implementing proof-of-stake that improve on most implementations and this report will end by examining Algorand in greater depth.   


##### Hashcash  

Hashcash was originally proposed by Adam Back in May 1997 [7] as a means to, "throttle systematic abuse of un-metered internet resources such as email and anonymous remailers." [2] The paper, 'Hashcash - A Denial of Service Counter-Measure' was written five years later in 2002 to provide an overview of the subsequent applications, proposed improvements and results from experiments involving what is called the, 'hashcash CPU cost-function'.  

Unlike other similar cost-functions known to the author at the time, hashcash is 'trapdoor-free'. A trapdoor-free cost function is defined as a cost function where the server has no advantage in minting tokens. [2] With most cost-functions, an opponent can easily create tokens, so asking for tokens to prevent things like spamming is not advantageous or beneficial for security. With hashcash and proof-of-work, only legitimate enitities would likely expend the effort needed to send messages. 

Interestingly, for the purposes of this report, one of the potential applications listed for hashcash is as a minting mechanism for the b-money electronic cash protocol famously proposed by Wei Dai [8] and generally regarded as a precursor to Bitcoin. Beck calls b-money, "an electronic cash scheme without a banking interface." [2]   

##### Bitcoin  

The first sentence of the Bitcoin white paper sums up the author's intent quite clealy: "A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without going through a financial institution." [1] Furthermore, Nakamoto talks about the need to prevent double-spending without a corresponding reliance on a trusted third party. There are a couple of weaknesses that are addressed concerning the trust based model. [1] 

For one, non-reversible transactions are never really possible as a central authority can not avoid mediating dispute. This truth drives up transaction costs and also serves to limit the minimum transaction size that is feasible inside of a payment system. This idea would later develop into a cornerstone of modern blockchain conversation - the idea of micro-transactions. Super small payments to help fuel economic progress that could allow for something like a decentralized video sharing site maybe where you could send someone a fraction of a penny if you like their how-to video on spotting toucans. 

Another weakness, and this relates to the fact that transactions are potentially reversible, is that the need for trust spreads throughout the system. Nakomoto cites the need for merchants to weary of customers. Merchants must ask for more information than what is needed. Because some fraud is unavoidable, the costs of this aggregated loss is mostly passed to consumers. As Nakomoto states, "cost and payment uncertainties can be avoided in person by using a physical currency" before pointing out that, "no mechanism exists to make payments over a communication channel without a trusted party." [1] Arguably Bitcoin has made this last statement a possibility - maybe in the future a fatal flaw will be found in the protocol and billions of dollars will go missing - and one major feature allowing for this is the concept of proof-of-work developed by Adam Back. [2]

Bitcoin is based on cryptographic proof instead of trust. By assembling blocks in a chain and connecting them all with the hash of the block that came before them, Bitcoin creates a web that is computationally infeasible to reverse. To reverse any transaction, a malicious actor would have to rebuild the blockchain faster than all of the honest nodes in the system combined. There is some economic protection against this type of behaviour because any entity or group of entities with more than 51% of all network mining power would have a large stake in the system and any major breach would cause prices to plummet.

##### Ethereum



##### References  

1. Nakamoto, Satoshi. "Bitcoin: A peer-to-peer electronic cash system." (2008).
2. Back, Adam. "Hashcash-a denial of service counter-measure." (2002).
3. Gilad, Yossi, Rotem Hemo, Silvio Micali, Georgios Vlachos, and Nickolai Zeldovich. "Algorand: Scaling byzantine agreements for cryptocurrencies." Proceedings of the 26th Symposium on Operating Systems Principles. 2017.
4. Wood, Gavin. "Ethereum: A secure decentralised generalised transaction ledger." Ethereum project yellow paper 151.2014 (2014): 1-32.
5. Buterin, Vitalik. "A next-generation smart contract and decentralized application platform." white paper 3.37 (2013).
6. Sompolinsky, Yonatan, and Aviv Zohar. "Secure high-rate transaction processing in bitcoin." International Conference on Financial Cryptography and Data Security. Springer, Berlin, Heidelberg, 2015.
7. Back, Adam. "Hashcash." (1997).
8. Wei Dai. b-money. Published at http://www.eskimo.com/ ̃weidai/bmoney.txt, Nov 1998.