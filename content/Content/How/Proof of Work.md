
## Prelude 

Let's start by examining the oldest [[Consensus Algorithm]], proof of work. In the next chapter, we will examine [[Proof of Stake]]. Before we get started, let's establish a framework to evaluate each. 

For each consensus algorithm, we should answer how each pillar of [[Resilience]] is fulfilled. 

![[Resilience]]

As noted in [[Blockchains Are Overrated]], all blockchain networks utilize the data-structure that is known as a blockchain to achieve **Auditable History**.

Achieving **Accessibility** is a subjective measure that is beyond what a baseline definition of consensus algorithm can normally achieve. An example of accessibility is that to play a role in the overall network (for example as a full node or an author), or to use any of application hosted by the network (for example a Decentralized Exchange), you should have *reasonable* ways to do so. Different blockchain systems adopt various measures to achieve this, and it falls outside of the baseline definition of a consensus algorithm. As one note-worthy  example, while Ethereum is by many standards known as an accessible blockchain, the OFAC regulations on authors has indeed caused limitation on this, and this is (at least with the current defined scope) outside of the role of a consensus algorithm.

Finally, we are left with **Verifiability** and **Reliability**. To root this back to our definitions in [[Execution, Ordering, History and State Machines]], this boils down to executing $F(x, y) \rightarrow y\prime$, the blockchain's STF correctly, such that other can be sure about this correctness with [[Trust#Science-based Trust]]. This topic is also intertwined with who are the [[Blockchain Networks#Authors]] and [[Blockchain Networks#Checkers]] of the system, as explained in [[Blockchain Networks]]. 
## Proof of Work
In an ideal blockchain network, anyone would be able to author new blocks. Assuming that the majority of node execute $F$ correctly, any malicious fork would also eventually resolve into the correct one. Yet, this gifts a severe spam vulnerability to the system. The idea of Proof of Work (which is borrowed from email spam protection) is to prevent this spam by introducing an amount of electrical power (work) that needs to be wasted, before anyone can submit a valid $F$. 

In proof of work, this involves appending an extra field to each block, called `nonce`, such that when the block is hashed, there are a number of leading zeros in the final 32 byte hash. The process of finding this right `nonce` is called **Mining** (see [[Miners and Validators]]), ergo the [[Blockchain Networks#Authors]] in such networks are called **Miners**.  In the Bitcoin network, the number of these prepending zeros is knowns as the **difficulty**. Finally, an entity's cumulative power to mine a valid `nonce` and create a new block is called the **Hashing Power**.

> [!info] A common practice in Proof of Work networks to allow a *large number of entities*, with small Hashing Power each, to come together and form one strong Miner is called [[Mining Pools]]. 

Crucially, while this mechanism prevents spam, it also introduces a secondary emergent property: *forging blocks with invalid $F$ in fact **cost money***. As the **difficulty** of the a proof of network increases, this cost only every increases. As noted above, without Proof of Work, the blockchain would still, in theory, could converge to the right fork as long as the the majority of Authors are honest. Yet, this doesn't work in practice because the cost of trying to attack the system would be negligible. Proof of Work is exactly a remedy this this: Making the cost of an attack to the system extremely high, such that we can consider it to be infeasible by any rational actor, in presence of honest majority authors.

Therefore, we can formulate a very important concept: [[Economic Security]]. That is, the **cost** of trying to attack a network, and force it to accept an invalid $F$ as valid. In Proof of Work networks, this cost is represented as electricity. For an entity to try and forge an invalid block, they would need to acquire an extremely high amount of hardware and electricity, which would make the attack infeasible.

So, to summarize, the reason we have we consider the execution of Bitcoin's STF to be correct and verifiable is [[Economic Security]]: The cost of an invalid STF, while the majority are not malicious, is extremely high. So high, that doing so would defy the purpose.

Also, to recap how a typical Proof of Work like Bitcoin operates: 
- All nodes can in principle be miners
- Yet, those who have more Hashing Power will be able to produce more blocks
- Therefore, to successfully attack the network, one would need to acquire (or bribe) the majority of the Hashing Power of the entire network.

[[Economic Security]] is an extremely important metric to evaluate the [[Resilience]] of a blockchain network upon. Moreover, understanding it will pave the way to [[Proof of Stake]], as it is essentially the same process, except instead of the cost being in the form of *wasting energy*, it is in the form of losing capital.