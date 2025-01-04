In [[Execution, Ordering, History and State Machines]] we modeled a blockchain as a state machine whose execution is [[Resilience]][^1]. In this chapter, we will look at the evolution of these state machines, and see what applications have so far been encoded as such.

This evolution can be categorized into two different eras, [[#Fixed State Machine]]
 and [[#Programmable State Machine]]. 
## Fixed State Machine

A fixed state machine blockchain is the simplest one; it has a set of rules that in principle never change. Moreover, this state machine has almost no way of being extended. 

The most famous example in this category is Bitcoin. Its state is merely the balance of users[^3], and its STF is a simple digital bank, and it offers no way to execute any further logic as a part of its STF[^2]. 

As noted, Bitcoin was a great demonstration that creating [[Trust#Science-based Trust]] is possible, but lacks any form of *extensibility*.
## Programmable State Machine

What if more blobs of code could be uploaded to the blockchain and stored as a part of its state, and these code blobs could be executed as the part of the STF? This gave birth to **programmable state machines**.
### Ethereum, EVM and Smart Contracts

Ethereum was the first blockchain to invent such a system. Its state machine was essentially that of Bitcoin (simple value transfer of the ETH token), *and* it allowed blobs of code, called **Smart Contracts**, to be uploaded into the blockchain state, and execute as a part of the STF, if a transaction triggered one. These blobs of code had to be in the format of **Ethereum Virtual Machine** (**EVM**) byte-code. The default language that could be compiled to EVM was **Solidity**, yet today more languages can target EVM. 

As an example, the transactions of the Bitcoin STF could only be similar to:
- `transfer(alice, bob, 1 BTC)`: transfer 1 BTC from Alice to Bob
Whereas the Ethereum's transactions could be either of:
- `transfer(alice, bob, 1 ETH)`: transfer 1 ETH from Alice to Bob
- `upload_contract(0x123..)`: upload a new contract with code `0x123..`.
- `call_contract(0x123, foo, bar)` call the (already uploaded) contract with code `0x123`'s method `foo` and pass `bar` as input.

Achieving this in a [[Resilience]] way is no easy feat, and similar to Bitcoin, Ethereum is a great demonstration that this is *possible*. The main challenges in achieving this are [[#Metering]] and [[#Determinisms]], discussed further below.

By and large, the majority of the blockchain ecosystem is (*still*, more than a decade after EVM's inception) focused on optimizing EVM as the main virtual machine on top of which the STF can be expanded. Yet, a number of projects have been pioneering new, more general, virtual machines as the extensible part of the STF.
### Polkadot: An STF that can host other blockchains
Polkadot is one such example. Instead of EVM, Polkadot chose a more general virtual machine (initially WebAssembly, later on an alteration of RiscV called PolkaVM) as a more flexible and extensible STF. 

This allowed Polkadot to not only run smart contracts (with relatively limited programmability), but also run/host an entire set blockchains within itself, giving birth to the idea of a *multi-chain blockchain network*.
### Polkadot JAM, ICP: An STF that can host any program
Yet, even hosting another blockchain in an advanced virtual machine such as RiscV is still a very limited degree of programmability. This is because a blockchain is still a [[State Machine]], confined to the boundaries of only being able to transition its state when new input (a *block* of transactions) comes in. 

In other words, a both a smart contract and a blockchain's code are primarily written as a set of callback functions (aka. transactions) that are triggered. A typical smart contract and/or blockchain transaction looks like:

```rust
/// A blockchain/smart-contract transaction
fn on_transaction(sender, input) -> Result<_, _> { .. }
```

Note that a blockchain is *slightly* more flexible than a smart contract. Given the high degree of *autonomy* that a blockchain has, its STF may include more flexible callbacks that are executed without the need of user input, for example on every block, or every n-th block, and similar: 

```rust
/// A more generic hook that is only readily possible in a blockchain
fn on_every_block(block_number: u32) -> Result<_, _> { .. }
```

But in both of the above, one can see what we mean by 

> ..confined to the boundaries of only being able to transition its state when new input (a *block* of transactions) comes in..

That is, it is hard to translate a computer program that is typically written as a normal `fn main() -> { .. }` into the above models. 

JAM, Polkadot next protocol upgrade, and ICP are two known projects[^4] that attempt to solve this, allowing for any program, simply written as a `fn main` to be uploaded into the blockchain, and executed as a part of the main STF, under all of the same [[Resilience]] properties of blockchain code execution. 

While fairly new, it is plausible that this invention would unlock a much larger group of applications into the work of [[Web3]]. 
## Appendices 
### Standalone Chains 
Another way to have programmable state machine, but in a one-off manner. But we are seeking a platform, a single blockchain that can host a diverse group of applications and more smaller STFs
### Upgradability 
Hard Foks
### Metering 
Executing untrusted code

### Determinisms 

## Summary

This built on top of the [[State Machine]] model explained in [[Evolution of Blockchain State Machines]], and described the evolution of these STFs.

Next, while we are still exploring *what* a blockchain is, we will look into the different roles in a blockchain system, and see who executes this STF, and exactly when. See [[Blockchain Networks]]. 

[^1]: How this [[Resilience]] is achieved is discussed more in the "How" section
[^2]: People have tried to extend Bitcoin with Ordinals and Bitcoin scripts, but they both extremely limited and we can set the aside for simplicity. 
[^3]: Stored in a format known as UTXO
[^4]: More might exist, yet I am not familiar with