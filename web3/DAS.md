
### Data Availability 

I have been exploring rollups and data availability for a while. And with this scalability solution the technique of Data Availability is a crucial piece to the entire architecture. 

Data Availability (DA) layer is designed to make data available to all network participants across a large number of nodes off the critical path of consensus. Instead, nodes are only required to download a small chunk of data, as opposed to the entire data blob associated with a block.


**Problems of DA in Monolithic blockchains?**
* Forcing a large number of network nodes to download, verify, and store the same data massively reduces throughput for blockchains.
* On-chain data storage also leads to exponential increases in the size of the blockchain, which further increases hardware requirements for full nodes that need to store an ever-increasing amounts of state.

**Why do we need DA**
* Freeing memory on main chain reducing congestion
* Storing more transactions in a single block
* Retrieval of data from block is much cheaper
* Cost efficient as lower transaction fees
* Interoparability between other chains
* Data analysis and bulk data 
* Faster development cycle

**What is process of DA?**
* Sharding - for modified on chain storage


---
### Data Availability Sampling (DAS)


DAS solves the need to verify the claim of availability of data in a block proposed by rollup sequencers on the settlement layer. 

The goal of DAS is to allow the download of fraction of data from the block instead of downloading the entire data set acting for validators as light node instead of full node. This saves data bandwidth issues and brings the cost of running hardware incredibly low. 

DAS relies on *erasure encoding* which is a cryptographic method that expands the given dataset with redundant data set in a such a manner that any half expanded data can be used to recover the original data.

With erasure coding a vector of (k) information chunks gets encoded into a (longer!) vector of  n coded chunks. The _rate_ R=k/n of the code measures the redundancy introduced by the code.

![table](../media/coding.png)

---

Sources:

https://www.paradigm.xyz/2022/08/das
https://ethereum.org/en/developers/docs/data-availability/
https://www.alchemy.com/overviews/data-availability-layer