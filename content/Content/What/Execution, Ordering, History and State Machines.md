[[What Is This All About?]] and [[Blockchain-based Authorities]] were mostly in abstract terms. In this chapter, we will concretely model these concepts into a tangible form, finishing our first big step towards *thinking clearly* about blockchains.

## Verifiable Execution
Authorities can be modeled as: 
- Having a set of rules
- Holding a contentious state 
- Performing mutations on the state based on what the rules say.

This can be re-modeled as a computer program: 
- The code of the program defines the rules
- The code has access to a persistent memory (state)
- Execution of the code updates the memory 

Another representation of this would be $F(x, y) \rightarrow y\prime$. 
- $F$ is the rule of the system, the program's *code*
- $y$ is the current state of the program's *input memory*
- $x$ is the *input* to the mutation
- $y\prime$ is the output of the mutation, the program's *output memory*

> For example, $F$ is the function that determines the rule of transfer of value in a digital bank, $x$ is a transfer, $y$ is the current balance of all users, and $y\prime$ is the balance of all users after the transfer. 

Then, you and I want to execute $F$ to perform a transfer, and agree upon a $y\prime$. Neither you nor I trust one another, and we need an [[Authority]] to execute $F$ for us.

We can either delegate this to [[Trust#Human-based Trust]] such as a normal bank, or delegate it to a blockchain (with programmability like Ethereum) to achieve [[Trust#Science-based Trust]].

**So, the first property of a blockchain is verifiable execution of code.** Knowing what $F$ is, we can be sure that it is being executed correctly

> TODO: what about open-source code on my server? 
## Ordering 

Then, imagine we have two subsequent transfers: 
- $F(x_1, y) \rightarrow y_1$ 
- $F(x_2, y) \rightarrow y_2$ 

And in both, $F$ is executed correctly. We still need to decide whether $y_1$ is correct or $y_2$.

> Imagine Alice has 10 dollars. $x_1$ is meant to credit 5 to Alice, and $x_2$ is meant to debit 12 from her. The second transfer is successful IFF $x_1$ happens before $x_2$, but not the other way.

So, we need to decide if the above mutations are: 
- $F(x_1, y) \rightarrow y_1$ , and then $F(x_2, y_1) \rightarrow y_{21}$  or
- $F(x_2, y) \rightarrow y_2$ , and then $F(x_1, y_2) \rightarrow y_{12}$ 

This is when we realize that a blockchain has to **not only execute a code correctly**, but also has to **determine the correct order of code execution**.

## Auditing
But is this enough? Yes and no. Suppose we are given the current state of the program, after $n$ mutations, $y_{n+1}$. Without any further means, we would have to trust that $F(x_0, y)$ all the way up until $F(x_n, y)$ has been executed correctly. If $F$ is executed using a [[Trust#Science-based Trust]], we can already be very sure that $y_{n+1}$ is indeed correct.

Yet, one great additional property of [[Trust#Science-based Trust]] is that, because it is based on hard sciences, it is **easily auditable**. As in, given the public and permissionless rules of the system, one can easily re-execute $F(x_0, y_0)$ all the way up to $F(x_n, y_n)$, and come to the conclusion that $y_{n+1}$ was indeed correct for themselves.

So, the third property of a blockchain based system is that **the entire history is auditable**.

> [!info] Genesis and Syncing
> 
> This is why in blockchain systems the notion of a genesis data and syncing is very prominent. We often hear the phrase "you can sync the blockchain". This means, given the initial state of the system, which is called "genesis" ($y_0$), and the known rule of the blockchain, $F$, you can always re-verify (*audit*) the entire history by executing $F(x_0, y_0)$ all the way up to $F(x_n, y_n)$.

Note that this is not always possible in the [[Trust#Human-based Trust]]. While audits and regulations are indeed a thing in for Human-based authorities, they rely on further Human-based trust to be verified[^1].
[^1]: the phrase "*who polices the police?*" encapsulates well why auditing a human-based trust often relies on further human-based trust. 

## State Machine
Finally, we can model the above 3 properties into a single mathematical model that encapsulates it all, a deterministic [state-machine](https://en.wikipedia.org/wiki/Finite-state_machine).

> ..a state machine is an abstract machine that **can be in exactly one of a finite number of states at any given time**. The state-machine can **change from one state to another** in response to some inputs; the change from one state to another is called a **transition**

Moreover, the rules of this change are defined as **State Transition Function (STF)**. Anyone can re-execute the state transition function from the initial state, and come to the same final state. 

So, to take our above example, $F(x, y) \rightarrow y\prime$, and model it as a state machine:
- $F$ is the state transition function
- $y$ is the current state
- $x$ is the *input* to the mutation
- $y\prime$ is the new state

```mehrmaid
graph LR
y["$y$"] -->|"$F(x,y)$"| yp["$y\prime$"]
```

## Blockchain Models
So far, we have used 3 models to demonstrate *what* blockchains actually achieve: 
1. As an authority, discussed in [[Blockchain-based Authorities]]
2. As a computer program with code and memory in [[Execution, Ordering, History and State Machines]]
3. As a deterministic state machine in [[Execution, Ordering, History and State Machines]]

We can summarize the terminology for each of these 3 models, alongside a few more details as follows:

![[Blockchain Models]]

## A Block
We may proactively borrow one piece of terminology that will be later explained in [[Blockchains Are Overrated]]. We have not formally described what a *blockchain* even is, and what the word block therefore means. 

At this point, it is safe to assume the following: 

A blockchain STF often processes inputs not one by one, but rather as a group of inputs, and these groups are called a **block**. A block, in other words, is a *block of transactions* that are bundled together. 
- $block = [tx_1, tx_2, tx_3]$
- and then the STF's invocation would be: $F(block, y) \rightarrow y\prime$

Also see [[Block and Header]].
## Summary
This chapter consolidated the 3 [[Blockchain Models]] mentioned above. With this model in mind, we can dive next into the [[Evolution of Blockchain State Machines]], and see what application logic has so far been encoded as a [[Resilience]] state machine. 