[[What Is This All About?]] and [[Blockchain-based Authorities]] were mostly in abstract terms. In this chapter, we will concretely model these concepts into a tangible form, finishing our first big step towards *thinking clearly* about blockchains.

## Verifiable Execution

As noted, authorities have a contentious state, and they are capable of performing mutations on it. This model is undeniably similar to that of a normal **computer program**. A program has some *code*, and the code has access to some form of persistent state. For simplicity, let's assume this is just a (persistent) *memory*. 

To model this, we can use the simple notation of $F(x, y) \rightarrow y\prime$. 
- $F$ is the rule of the system, the program's *code*
- $y$ is the current state of the program's *input memory*
- $x$ is the *input* to the mutation
- $y\prime$ is the output of the mutation, the program's *output memory*

For example, $F$ is the function that determines the rule of transfer of value in a digital bank, $x$ is a transfer, $y$ is the current balance of all users, and $y\prime$ is the balance of all users after the transfer. 

Then, you and I want to execute $F$ to perform a transfer, and agree upon a $y\prime$. Neither you nor I trust one another, and as noted in [[Need For Trust]], we need an [[Authority]] to execute $F$ for us.

We can either delegate this to [[Trust#Human-based Trust]], or delegate it to a blockchain (with programmability like Ethereum) to achieve [[Trust#Science-based Trust]]. 

**So, the first property of a blockchain is verifiable execution of code.**

## Ordering 

Then, imagine we have two subsequent transfers: 
- $F(x_1, y) \rightarrow y_1$ 
- $F(x_2, y) \rightarrow y_2$ 

And in both, $F$ is executed correctly. We still need to decide whether $y_1$ is correct or $y_2$.

> Imagine Alice has 10 dollars. $x_1$ is meant to credit 5 to Alice, and $x_2$ is meant to debit 12 from her. The second transfer is successful IFF $x_1$ happens before $x_2$, but not the other way.

So, we need to decide if the above mutations are: 
- $F(x_1, y) \rightarrow y_1$ , and then $F(x_2, y_1) \rightarrow y_{21}$  or
- $F(x_2, y) \rightarrow y_2$ , and then $F(x_1, y_2) \rightarrow y_{12}$ 

This is when we realize that an authority has to **not only execute a code correctly**, but also has to **determine the correct order of code execution**.

## Auditing

But is this enough? Yes and no. Suppose we are given the current state of the program, after $n$ mutations, $y_{n+1}$. Without any further means, we would have to trust that $F(x_0, y)$ all the way up until $F(x_n, y)$ has been executed correctly. If $F$ is executed using a [[Trust#Science-based Trust]], we can already be very sure that $y_{n+1}$ is indeed correct. 

Yet, one great additional property of [[Trust#Science-based Trust]] is that, because it is based on hard sciences, it is **easily auditable**. As in, given the public and permissionless rules of the system, one can easily re-execute $F(x_0, y_0)$ all the way up to $F(x_n, y_n)$, and come to the conclusion that $y_{n+1}$ was indeed correct. 

So, the third property of a blockchain based system is that **the entire history is auditable**.

> [!info] Genesis and Syncing
> 
> This is why in blockchain-based systems the notion of a genesis data and syncing is very prominent. We often hear the phrase "you can sync the blockchain". This means, given the initial state of the system, which is called "genesis" ($y_0$), and the known rule of the blockchain, $F$, you can always re-verify (*audit*) the entire history by executing $F(x_0, y_0)$ all the way up to $F(x_n, y_n)$.


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

Or to demonstrate our dilemma with respect to ordering: 

```mehrmaid
graph LR
y["$y$"] -->|"$F(x_1, y)$"| y1["$y_1$"] -->|"$F(x_2, y_1)$"| y2["$y_{12}$"]
```
or 
```mehrmaid
graph LR
y["$y$"] -->|"$F(x_2, y)$"| y1["$y_2$"] -->|"$F(x_1, y_2)$"| y2["$y_{21}$"]
```

## Blockchain Models

So far, we have used 3 models to demonstrate *what* blockchains actually achieve: 
1. As an authority, discussed in [[Blockchain-based Authorities]]
2. As a computer program with code and memory in [[Execution, Ordering and History Yields State Machine]]
3. As a deterministic state machine in [[Execution, Ordering and History Yields State Machine]]

We can summarize the terminology for each of these 3 models, alongside a few more details as follows:

![[Blockchain Models]]

## Summary

TODO
- Authorities have contentious state, and perform verifiable mutations on it. We can be pretty sure that this mutation was then correct.
- This is very similar to a computer program with a memory. `f` is the code, `x` is the input, and `y`is the output memory after executing `f(x)`.
- Imagine some computer program exists `f(x) -> y`. You and I need to establish trust on what Y is. You don't trust me to execute `f`, nor do I trust you to execute `f`. So, we either give `f` to an authority with human-based trust to execute it for us, or we give it to a blockchain like Ethereum to execute it for us. And we know that the execution in Ethereum is also correct. So this is "Verifiable execution of code". 
- But what if there are two branches of history, which conflict with one another, but each are correct in their own branch? 
- This is why verifiable execution is not enough, you also need to figure out the ordering, and from ordering you can derive the full history.  
- All of this can be modeled as a"**State Machine**