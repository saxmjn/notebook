
### Data Availability Sampling 

I have been exploring rollups and data availability for a while. And with this scalability solution the technique of Data Availability Sampling is a crucial piece to the entire architecture. 

DAS solves the need to verify the claim of availability of data in a block proposed by rollup sequencers on the settlement layer. 

The goal of DAS is to allow the download of fraction of data from the block instead of downloading the entire data set acting for validators as light node instead of full node. This saves data bandwidth issues and brings the cost of running hardware incredibly low. 

DAS relies on erasure encoding which is a cryptographic method that expands the given dataset with redundant data set in a such a manner that any half expanded data can be used to recover the original data.

With erasure coding a vector of (k) information chunks gets encoded into a (longer!) vector of  n coded chunks. The _rate_ R=k/n of the code measures the redundancy introduced by the code.

---

Sources:

https://www.paradigm.xyz/2022/08/das
https://ethereum.org/en/developers/docs/data-availability/
https://www.alchemy.com/overviews/data-availability-layer