
### Layer2 Scalability

The main goal of scalability is to increase transaction speed (faster finality), and transaction throughput (high transactions per second), without sacrificing decentralization or security. 

The layer2 solution batches transactions into groups before anchoring them to layer 1, after which they are secured by layer 1 and cannot be altered.

----

##### State channels

----

##### Sidechains:
A sidechain is an independent EVM-compatible blockchain which runs in parallel to Mainnet. These are compatible with Ethereum via two-way bridges, and run under their own chosen rules of consensus, and block parameters.

----

##### Plasma chains

----
##### Validiums

----

##### Optimistic [[Rollups]]: 
Assumes transactions are valid by default and only runs computation, via a **fraud proof**, in the event of a challenge.

Optimistic rollups execute transactions outside of Ethereum, but post transaction data to Mainnet as `calldata`. Optimistic rollups also use compression techniques to reduce the amount of data posted on Ethereum.

----
##### ZK Rollups: 
runs computation off-chain and submits a **validity proof** to the main chain. 

zk-SNARKs (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge)
zk-STARKs (Zero-Knowledge Scalable Transparent ARgument of Knowledge)

https://consensys.io/blog/zero-knowledge-proofs-starks-vs-snarks
-----
