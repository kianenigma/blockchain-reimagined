- Blockchain as **authority**
	- State 
	- Rules of the authority
	- Mutation 
- Blockchain as **deterministic state machine**
	- State
	- State transition function
	- Transition
- Blockchain as a **computer program**
	- Memory (state)
	- Code
	- Input 

Inputs may be called **transaction**, borrowed from the database industry, or **Extrinsic Data**, borrowed from the [Polkadot](https://polkadot.com) jargon.

The keyword **transaction** is very popular, yet it is mostly used when a user signs some information and inputs it to the blockchain. This jargon is enough for simpler blockchains that only allow this one type of transition in their STF. Yet, it is insufficient to describe: 
- What if the input was *not* signed by a user? This is mainly why Polkadot chose the broader term *Extrinsic Data* as opposed to *Transaction*.
- What if transition happened as an *automatic* mutation, and not as a consequence of any external data? This is why Transition or Mutation are more general terms. 

