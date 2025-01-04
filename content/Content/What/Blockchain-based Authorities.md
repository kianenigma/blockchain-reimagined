[[What Is This All About?]] briefly touched upon the nature of [[Trust]] and [[Authority]]. We described how Bitcoin is creates a trustworthy digital bank, and briefly touched upon Ethereum, creating a global trustworthy digital computer that can perform general computations. Yet, we closed the chapter by acknowledging that there are limitations to this model.

In this chapter, we will build a model around what those limitations are.
## State and Mutation

Most authorities can be abstracted as two functions: They hold value-bearing and contentious ***state*** (information), and they perform ***mutations*** upon that state.

```mermaid
flowchart
Auth[Authority] --> State
Auth --> Mutation
```

In the example of owning digital money in [[What Is This All About?]], the state of the authority is the ledger of all accounts and balances, and the mutations are transfers between two accounts. 
## Digital and Real World 

Another property of authorities is whether the state that they hold, and the mutations that are done upon it, are in the ***real world***, or the ***digital world***. 

```mermaid
flowchart
	Auth[Authority] --> RW[Real World]	
	Auth --> Digital[Digital World]
```

**Banking**, excluding cash, and many similar financial services, are examples of authorities that are purely **digital**. The state is a ledger holding everyone's balance, which is merely a set of numbers in a computer. Updating one's balance is as simple as updating one of these numbers.

Conversely, the **land registry** is a **real world form of authority**. Such an authority needs to be able to know if a land exists, who owns it, and crucially, enforce the ownership of it through some law enforcement mean, if need be.

![[Proposition - Oracle Problem in Authorities]]
### Oracle Problem 
The often overlooked reality is: Blockchains, as discussed so far, are obviously digital systems. **For a digital system, introspection of the real world is (nearly) impossible to do *independently***. This difficulty, specifically when it comes to reading information from the real world, is referred to as the [[Oracle Problem]].

```mermaid
flowchart
	DS[Digital System] --"write ❌"--> RW[Real World] --"read ❌"--> DS	
```

As an example, a digital system, such as a Blockchain, has no practical way to *independently* understand if a piece of land exists, and to whom it belongs. Moreover, a digital system cannot meaningfully enforce that "*Alice should from now on own this land that formerly belonged to Bob*".

> [!TIP] Real World Asset Fallacy 
> A very common fallacy in the blockchain space is applications that create a blockchain, selling its [[Resilience]], but they have a clear bottleneck in which a centralized authority need to sit in between the blockchain and the outside world, and solve the [[Oracle Problem]]. I believe a lot of companies aiming to bring real-world-assets into blockchains are fundamentally mislead by overlooking this fact. 

This is why real world authorities are backed by some form of ***law enforcement unit***, such as the police and military, as noted in [[What Is This All About?]]. No blockchain based system yet has a real world law enforcement body behind it[^1].

[^1]: The Network State book proposes steps through which digital authorities can evolve into gaining legitimacy in the real world, which is very much related to the enforcement issue mentioned above.

Contrary, blockchains can effortlessly harvest their full [[Resilience]] on use-cases whose state is purely digital. **This property demonstrates why Decentralized Finance (DeFi henceforth) is such a successful use-case for blockchains**. Assuming a free and open internet[^2] upon which information can be exchanged, DeFi requires no further substrate to operate upon. 

[^2]: How accurate is this assumption of the internet being "free"? See [[The Free Internet|here]]. 

### Weakest Link

This is NOT to say that no blockchain based system should attempt to tackle any real-world use-case. But, we should acknowledge that there is a high chance to create a system with a single-point-of-failure here.

Very often, such systems combine a blockchain and its science-based trust with a human-based authority that conveys the existence of real-world information to and from the blockchain, and this human-based authority is exactly the single point of failure[^3]. This design might suffer from the weakest link issue: 

![[Proposition - Weakest Link]]
## Summary 

Any [[Authority]]'s role is to establish [[Trust]]. Blockchains are systems that yield [[Resilience]] science-based trust, instead of the old-school human-based trust. 

An authority typically needs to hold some contentious state and perform mutations on top of it. This state is either in the real world or the digital world. 

Digital state is a great fit for blockchains, since it can be easily mutated. Real world matters are more difficult, due to the [[Oracle Problem]]. 

While we can strive to solve the [[Oracle Problem]] in a [[Resilience]] manner, turning a blind eye to it will likely create more damage than harm, as it is a [[Proposition - Weakest Link|single point of failure]] for a system. 

[^3]: In some sense, I am debunking the entire class of "*Let's tokenize this Rolex and put it on a blockchain*" ideas, or at least claiming that they are a big compromise in [[Resilience]]. There is no meaningful way for a blockchain to know about the existence of a Rolex, other than introducing another form of human-based authority/oracle that needs to be trusted.