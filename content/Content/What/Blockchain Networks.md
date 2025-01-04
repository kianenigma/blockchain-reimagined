So far, we have [[Blockchain Models|modeled]] a blockchain as either a computer program or a state-machine. Yet, we have not discussed ***who executes the STF and when***. We have also referred to such systems as *blockchain systems*. Let's correct course by rephrasing this into a *blockchain network*.

A *network* is a connected set of *nodes*, with different nodes possibly having different roles. 

So, let's see what these roles typically are, and when do each execute the STF. 
## Authors  
First, we have the set of nodes that can actually author a new block, and publish it to the network for everyone else. 

In networks like Bitcoin and early day Ethereum, all nodes can *in principle* be an author, although their chances of actually authoring a block might be near zero. In Bitcoin, the authors are called *miners*. 

In most [[Proof of Stake]] networks like  and Polkadot, a subset of nodes are periodically elected as the *set of authors*, and for a period of time (known as an *Epoch*) rotate the authorship role among themselves. Once the epoch is over, a new set is elected and so on. 

As noted, one of the roles of the [[Consensus Algorithm]] is to select who should be the next block author.

> [!Info]  [[Consortium Blockchains]]
> A blockchain may have a closed set of nodes that perform the [[Consensus Algorithm]] and is known as a [[Consortium Blockchains]]. Such networks only offer a subset of the [[Resilience]] aspects. 

Block authors usually have some sort of a *transaction queue* within themselves, which is a queue of all transactions (mutations) that are pending to be applied. When each of them gets a chance to author a block, they execute a subset of transactions (based on their preference, for example transactions that pay the most fee) using the STF, bundle them in a block, and share it with the rest of the network. 

### Checkers 

A subset of nodes might be tasked to actively **check** the work of the authors, and report any misbehavior. In other words, ensure that in a given mutation $F(block, y) \rightarrow y\prime$, $F$ was indeed executed correctly, among ensuring the correct order, as explained in [[Execution, Ordering, History and State Machines]]. 

This is also one of the rules that the [[Consensus Algorithm]] of a blockchain must define. In some systems, there are no checkers, and it is merely assumed that diverging from the correct execution and ordering rules has enough economic disincentive. In others, these misbehaviors are explicitly reported and an economical slash happens to further punish diverging from $F$.  

### Aside: Proposer Builder Separation (PBS).

Predominantly in Ethereum, the task of finding the most *efficient* block to propose is further decoupled from the [[#Authors]], and is given to a market of other nodes that are actively searching and bidding for the best block to produce, called **Proposers**.

This is an implementation detail and does not alter the role of [[#Authors]] and [[#Checkers]] mentioned above. At the end of the day, Authors must *somehow* find a good block to propose. They either do that by looking at their transaction queue themselves, or by delegating this task to a proposer. 

## Full Node 
Full nodes are the ones that are following the work of the authors by re-executing the STF based on proposed blocks, but don't actively participate in creation of new blocks. 

For a network to have [[Resilience]], it is utmost important for a full node software to be available, not need sophisticated hardware to run on, and be able to successfully sync the entire blockchain from genesis all the way to the tip of the chain. 

This would the consequently allow anyone to verify any (old) state (e.g. *how much BTC I had a year ago, and today?*) which was one of the properties of [[Trust#Science-based Trust]]. 
## Archive Nodes 
Full nodes typically store the entire history of transactions, but discard intermediate states. Because, given the correct $F$, the genesis state $y_0$, and the sequence of $[block_0, block_1, ..., block_n]$, they can recreate any of the intermediate state $y_n$ by re-executing the sequence of:
- $F(block_0, y_0) \rightarrow y_1$
- $F(block_1, y_1) \rightarrow y_2$ 
- $...$
- $F(block_{p_1}, y_{n-1}) \rightarrow y_n$

If a node decides to store all of the intermediate states, it is typically called an archive node.
## RPC Node 
Either a full node or an archive node that decides to expose its database (of most notably $[block_0, block_1, ..., block_n]$ and $[y_0, y1, ..., y_n]$) over RPC is called an RPC node. 

Crucially, an RPC node that merely replies to queries into its database with the raw answer is not particularly [[Resilience]]. This is because there is no easy way for the one asking the query to verify the result.  

This is why the theoretically ideal scenario for connecting for a blockchain network is for each user to have their own full node running locally, such that they don't need to rely on an external RPC node. Yet, this is not a feasible scenario for user experience, and is generally addressed by using [[#State Proofs]] within a [[#Light Node]], explained next. 
## State Proofs 
One way to fix the problem with [[#RPC Node]] is to use what is known as a [[State Proof]]. State proofs are cryptographic proofs of any given query over the state that are sent alongside the response, allowing the recipient to have absolute guarantee about the correctness of that response.

This is further explained in [[State Proof]]. 
## Light Node 
Light nodes are similar to full nodes in that they are not actively participating in authoring, and are merely following the chain. Yet, to save resources, they don't re-execute the STF at every single block. Instead, they only follow the *block headers*. Within the header, they have access to the cryptographic hashed that are necessary to query any further data using [[State Proof]]. 

Running a light node and relying on state proofs is crucial to ensure [[Resilience]], especially in environments that have constrained resources, such as a mobile phone, a web page, or an embedded device, where running a [[#Full Node]] is not feasible. 

> TODO: we have not yet explained what a block header is. 

## Summary 
This is the last chapter in which we describe *what* blockchain networks are, and what properties they have. 

We will revisit the concepts described here once we explain the How part of blockchains further, namely when we describe how two common [[Consensus Algorithm]] work, [[Proof of Work]] and [[Proof of Stake]]. 
