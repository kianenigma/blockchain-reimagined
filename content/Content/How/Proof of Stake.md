As noted in the final part of [[Proof of Work]], when seen from the lens of [[Economic Security]], Proof of Stake is more or less the same as [[Proof of Work]], except it utilizes a *less wasteful* method to achieve verifiable execution of STF.

Jumping right into it, Proof of Work requires: 
- Any participant in the network to lock an amount of capital in a vault inside the protocol, where they themselves can no long access it
- In the event that is known they diverged from the STF, This capital is **slashed**

In a very similar manner to [[Proof of Work]], Proof of stake is a more pure form of achieving verifiable execution through [[Economic Security]], leading to [[Resilience]]. Because all authors are asked to lock a (hopefully significant) amount of capital *at stake* (therefore the name Proof of *Stake*), we can be sure that they execute the STF correctly and not diverge from the protocol.

Most Proof of Stake networks utilize their own value-bearing tokens to be staked, therefore the act of "*Staking*" is usually named as one of the utilities of that token. In principle though, the staked token can be anything that bears value, even USDT. 

Some proof of work networks literally allow anyone to be a block author, yet the likelihood of them being selected as the author is proportional to their amount at stake. Others deploy a different approach where the top $N$ -strongly-backed-authors are selected as an *authoring committee*, and this committee members will then take turn in authoring new blocks. 

A few extra useful pieces of terminology that is more relevant to Proof of Stake:
- Authors and Checkers are called Validators (see [[Miners and Validators]]).
- Entities are allowed to contribute to the [[Economic Security]] of a validator, while not running an authoring node are called [[Delegators or Nominators]], depending on the implementation. 

Similar to how the cost of effectively attacking a [[Proof of Work]] network is to acquire the majority of the Hashing Power, in Proof of Stake networks, the cost is to obtain majority of the network staked tokens, and use them to force an invalid STF. 
## Blockspace And Quality Thereof
First, let's introduce a new keyword: [[Blockspace]]. It is a measure of the amount of verifiable computation (STF) that a blockchain can perform, namely by the authors.

Having seen how [[Proof of Work]] and Proof of Stake work, we can assert that a blockchain should not be evaluated only by the quantity of its blockspace, but also based on the quality of it. 

To be more precise, the quality of [[Blockspace]] is proportional to the amount of [[Economic Security]] backing it, because Economic Security is the essence of why that block(space) is verifiable to begin with.
