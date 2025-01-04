A group of inputs, transactions, or extrinsic data, based on which [[Blockchain Models]] we are using, bundled together. 

A block also contains an important header, which links it using a [[Cryptographically Secured Hash]] to a specific **parent block**, creating the tamper-proof property of the blockchain data structure. See [[Blockchains Are Overrated]] for more detail. 

Other than linking to a parent block, the header also contains secure hashes that act as a digest or commitment to:
- What entire transactions that are in the block
- The posterior state after executing this block

These commitments, combined with [[State Proof]], can allow anyone to securely query information about the transactions and the state of this block. 