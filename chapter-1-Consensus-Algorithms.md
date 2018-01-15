# Consensus Algorithms

[ntroduction to Hyperledger Business Blockchain Design Philosophy and Consensus](https://www.hyperledger.org/wp-content/uploads/2017/08/HyperLedger_Arch_WG_Paper_1_Consensus.pdf)

Consensus in the network refers to the process of achieving agreement among the network participants as to the correct state of data on the system. Consensus leads to all nodes sharing the exact same data. A consensus algorithm, hence, does two things: it ensures that the data on the ledger is the same for all the nodes in the network, and, in turn, prevents malicious actors from manipulating the data. The consensus algorithm varies with different blockchain implementations.

While the Bitcoin blockchain uses Proof of Work as the consensus algorithm, other blockchains and distributed ledgers are deploying a variety of consensus algorithms, like the Proof of Stake, Proof of Burn, Proof of Capacity, Proof of Elapsed Time, and many others, depending on their unique requirements.

Next, we will briefly explain some of these algorithms.

## Proof of Work (PoW)

The Proof of Work consensus algorithm involves solving a computational challenging puzzle in order to create new blocks in the Bitcoin blockchain. Colloquially, the process is known as 'mining', and the nodes in the network that engage in mining are known as 'miners'. The incentive for mining transactions lies in economic payoffs, where competing miners are rewarded with 12.5 bitcoins and a small transaction fee.

As described in the 2016 Kudelski Security report,

"Proof-of-work (PoW) is the outcome of a successful mining process and, although the proof is hard to create, [it] is easy to verify."

For better understanding, please consider the following example provided by Ofir Beigel:

"(...) guessing a combination to a lock is a proof to a challenge. It is very hard to produce this since you will need to guess many different combinations; but once produced, it is easy to validate. Just enter the combination and see if the lock opens".

Multiple criticisms exist for the PoW consensus algorithm. PoW requires a huge amount of energy to be expended, given the computationally heavy algorithm. In addition, PoW has a high latency of transaction validation, and the concentration of mining power is located in countries where electricity is cheap. In terms of the network security, PoW is susceptible to the '51% attack', which refers to an attack on a blockchain by a group of miners controlling more than 50% of the network's computing power.

## Proof of Stake (PoS)

The Proof of Stake algorithm is a generalization of the Proof of Work algorithm. In PoS, the nodes are known as the 'validators' and, rather than mining the blockchain, they validate the transactions to earn a transaction fee. There is no mining to be done, as all coins exist from day one. Simply put, nodes are randomly selected to validate blocks, and the probability of this random selection depends on the amount of stake held. So, if node X owns 2 coins and node Y owns 1 coin, node X is twice as likely to be called upon to validate a block of transactions. The specific implementation of PoS can vary, depending on the use case, or as a matter of software design. Instances include [Proof of Deposit](https://www.linkedin.com/pulse/blockchain-consensus-algorithm-proof-of-work-satyakam-chakravarty/) and [Proof of Burn](https://en.bitcoin.it/wiki/Proof_of_burn). The PoS algorithm saves expensive computational resources that are spent in mining under a PoW consensus regime.

## Proof of Elapsed Time (PoET)

Developed by Intel, the Proof of Elapsed Time consensus algorithm emulates the Bitcoin-style Proof of Work. Hyperledger's Sawtooth implementation is an example of PoET at work. Instead of competing to solve the cryptographic challenge and mine the next block, as in the Bitcoin blockchain, the PoET consensus algorithm is a hybrid of a random lottery and first-come-first-serve basis. In PoET, each validator is given a random wait time.

"The validator with the shortest wait time for a particular transaction block is elected the leader."

- [sawtooth.hyperledger.org](sawtooth.hyperledger.org)

This "leader" gets to create the next block on the chain.

## Simplified Byzantine Fault Tolerance (SBFT)

The Simplified Byzantine Fault Tolerant consensus algorithm implements an adopted version of the [Practical Byzantine Fault Tolerant](https://blog.acolyer.org/2015/05/18/practical-byzantine-fault-tolerance/) (PBFT) algorithm, and seeks to provide significant improvements over Bitcoin's Proof of Work consensus protocol. The basic idea involves a single validator who bundles proposed transactions and forms a new block. Note that, unlike the Bitcoin blockchain, the validator is a known party, given the permissioned nature of the ledger. Consensus is achieved as a result of a minimum number of other nodes in the network ratifying the new block. In order to be tolerant of a Byzantine fault, the number of nodes that must reach consensus is 2f+1 in a system containing 3f+1 nodes, where f is the number of faults in the system. For example, if we have 7 nodes in the system, then 5 of those nodes must agree if 2 of the nodes are acting in a faulty manner.

The practical example would be that of ByzCoin, which seeks to make key improvements over the original Bitcoin protocol. Addressing the challenge around scalability due to high latency, ByzCoin transactions are irreversibly committed to the blockchain within seconds. The added advantage is the communication trees to "(...) optimize transaction commitments and verification under normal operations." (2016 Kudelski Security report).

## Proof of Authority (PoA)

Proof-of-Authority (PoA) is a consensus algorithm which can be used for permissioned ledgers. It uses a set of 'authorities', which are designated nodes that are allowed to create new blocks and secure the ledger. Ledgers using PoA require sign-off by a majority of authorities in order for a block to be created.

