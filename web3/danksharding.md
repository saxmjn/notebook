
## Danksharding: EIP-4488 and EIP-4844

Danksharding is the full realization of the rollup scaling for Ethereum, turning it into a unified settlement and data availability layer. It was introduced as a part of Ethereum's rollup centric roadmap in 2020. 

The implementations planned as part of Danksharding are:
* PBS (proposer/builder separation), to avoid requiring individual validators to process 32 MB of data in one slot.
* Merged Free Markets
* Data Availability Sampling
* Blob Transaction

These implementations are required to be in consensus-layer, and does not require any additional work from execution client.


> [!info]
> #### Sharding before Danksharding
> Sharding is splitting up the Ethereum blockchain so that subsets of validators are only responsible for a fraction of the total data. This was originally intended to be the way for Ethereum to scale. However, layer 2 rollups have developed much faster than expected and have provided a lot of scaling already, and will provide much more after Proto-Danksharding is implemented. This means "shard chains" are no longer needed and have been dropped from the roadmap.

> [!info]
> #### Why does Danksharding require Proposer Builder Seperation?
> 
> Proposer-builder separation is required to prevent individual validators from having to generate expensive commitments and proofs for 32MB of blob data. This would put too much strain on home stakers and require them to invest in more powerful hardware, which hurts decentralization. Instead, specialized block builders take responsibility for this expensive computational work. Then, they make their blocks available to block proposers to broadcast. The block proposer simply chooses the block that is most profitable. Anyone can verify the blobs cheaply and quickly, meaning any normal validator can check that the block builders are behaving honestly. This allows the large blobs to be processed without sacrificing decentralization. Misbehaving block builders could simply be ejected from the network and slashed - others will step into their place because block building is a profitable activity.


---
### EIP-4844 : Proto-Danksharding

Proto-Danksharding, also known as [EIP-4844(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844), is a way for [rollups](https://ethereum.org/en/layer-2/#rollups) to add cheaper data to blocks. It is an intermediately step to make txns on L2s cheaper and scale ethereum for > 100,000 tps. 

> [!Info]
> The name comes from the two researchers who proposed the idea: Protolambda and Dankrad Feist. Checkout conversation b/w Vitalik, Protolambda and Dankrad about Danksharding 
> https://www.youtube.com/watch?v=N5p0TB77flM

The main feature introduced by proto-danksharding is new transaction type, which we call a **blob-carrying transaction**. Before this, rollups had been limited in how cheap they can make user transactions by the fact that they post their transactions in `CALLDATA`.

Cons of CALLDATA:
* Data passed as CALLDATA lives on chain forever even though they are required only for a short period during fraud proof. 

Pros for BlobData:
* Data passed as a blobdata is not accessible to EVM execution and EVM can only view the commitment to the blob.
* At the node-level, the blobs of data are held in the consensus client.
* Blobs are extremely large (~125Kb) and much cheaper than CALLDATA as it is not competing for gas. 
* Data in blobs are temporary and are deleted approximately after 4096 epochs (18days ~ 2eeks)

---
> [!info]
> ##### Why is it OK to delete Blob Data?
> Rollups post commitments to their transaction data on-chain and also make the actual data available in data blobs. This means provers can check the commitments are valid or challenge data they think is wrong. At the node-level, the blobs of data are held in the consensus client. The consensus clients attest that they have seen the data and that it has been propagated around the network. If the data was kept forever, these clients would bloat and lead to large hardware requirements for running nodes. Instead, the data is automatically pruned from the node every 18 days. The consensus client attestations demonstrate that there was a sufficient opportunity for provers to verify the data. The actual data can be stored off-chain by rollup operators, users or others.

---
### EIP-4488

Before EIP-4844 there was another simpler attempt called EIP-4488. The purpose of EIP-4488 was to greatly decreases the gas cost of transaction CALLDATA and simultaneously caps total transaction CALLDATA in a block.

EIP-4488 did this with two simple rules:

- Calldata gas cost reduced from 16 gas per byte to 3 gas per byte
- A limit of 1 MB per block plus an extra 300 bytes per transaction (theoretical max: ~1.4 MB)

![table](../media/sc-1.png)

> [!info]
> #### Why there was a cap on max CALLDATA per block in EIP-4488?
> Today, the average block size [is 60-90 kB](https://etherscan.io/chart/blocksize), but the _maximum_ block size is `30M / 16 = 1,875,000` bytes (plus about a kilobyte of block and tx overhead). Simply decreasing the calldata gas cost from 16 to 3 would increase the maximum block size to 10M bytes. This would push the Ethereum p2p networking layer to unprecedented levels of strain and risk breaking the network; some previous live tests of ~500 kB blocks a few years ago had already taken down a few bootstrap nodes. So it was viable to cap it to 1.4 worst case block size while preventing most of the security risk.

---

#### Blobs

> [!info]
> Blobs are 4096 field-elements of 32 bytes each, with a long term maximum of 16 blobs per block. 4096 * 32 bytes * 16 per block = 2 MiB (One mebibyte equals 1.048576 megabytes) per block maximum. The blob cap per block can start low and grow over multiple network upgrades. Because validators and clients still have to download full blob contents, data bandwidth in proto-danksharding is targeted to 1 MB per slot. 

##### Blob Transaction 

The new type of EIP-2718 transaction, “blob transaction”, where the TransactionType is `BLOB_TX_TYPE` = `Bytes1(0x03)`. The fields `chain_id`, `nonce`, `max_priority_fee_per_gas`, `max_fee_per_gas`, `gas_limit`, `value`, `data`, and `access_list` follow the same semantics as EIP-1559.

The field `max_fee_per_blob_gas` is a `uint256` and the field `blob_versioned_hashes` represents a list of hash outputs from`kzg_to_versioned_hash`.

![table](../media/blobTx.png)