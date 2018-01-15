# Addressing Illegal, Unregulated, and Unreported Tuna Fishing (Demonstrated Scenario)

## Defining Our Actors

- Sarah is the fisherman who sustainably and legally catches tuna.
- Tuna processing plant processes and bags the tuna after they have been caught.
- Regulators verify that the tuna has been legally and sustainably caught.
- Miriam is a restaurant owner who will serve as the recipient in this situation.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/3deee7052b123b20c15de7aaf7c3d3fc/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/2_-__Sawtooth__Demonstrated_Scenario__1_.jpg)

## Featured Hyperledger Sawtooth Elements

Transaction validators validate transactions.

Transaction families are smart contracts in Hyperledger Sawtooth. They define the operations that can be applied to transactions. Transaction families consist of both transaction processors (the server-side logic) and clients (for use from Web or mobile applications).

Transaction processor is the server-side business logic of transaction families that acts upon network assets.

Transaction batches are clusters of transactions that are either all committed to state or are all not committed to state.

The network layer is responsible for communicating between validators in a Hyperledger Sawtooth network, including performing initial connectivity, peer discovery, and message handling.

Global state contains the current state of the ledger and a chain of transaction invocations. The state for all transaction families is represented on each validator. The process of block validation on each validator ensures that the same transactions result in the same state transitions, and that the resulting data is the same for all participants in the network. The state is split into namespaces, which allow flexibility for transaction family authors to define, share, and reuse global state data between transaction processors.

## Why Sawtooth?

Miriam is a restaurant owner looking to source high quality tuna, that have been caught responsibly. Whenever Miriam buys tuna, she cannot be sure whether she can trust that the tuna she is purchasing is legally and sustainably caught, given the prominence of illegal and unreported tuna fishing. Luckily, Hyperledger Sawtooth can help!

Hyperledger Sawtooth is ideal for this scenario because of its ability to track an asset's (in this case tuna) provenance and journey. The ability to batch transactions together allows for all tuna within a catch to be entered as a whole. The distributed state agreement, novel consensus algorithm, and decoupled business logic from the consensus layer allow Miriam to be confident that she is buying tuna that has been legally caught.

## The Supply Chain

Hyperledger Sawtooth is extremely scalable and able to withstand high throughput of data, which makes it a great option for production supply chain scenarios.

We will start with Sarah, our licensed tuna fisher, who sells her tuna to multiple restaurants. Sarah operates as a private business, in which her company frequently makes international deals. Through an application, Sarah is able to gain entry to a Hyperledger Sawtooth blockchain network comprised of other fishermen, as well as processing plants, regulators, and restaurant owners. Sarah, as  well as the processing plants, have the ability to add and update information to this ledger as tuna passes through the supply chain, while regulators and restaurants have read access to ledger records.

## The Tuna Asset

With each catch, Sarah records some information about each individual tuna, including: a unique ID number, the location and time of the catch, its weight, and who caught the fish. For the sake of simplicity, we will stick with these data attributes. However, in an actual application, many more details would be recorded, from toxicology, to other physical characteristics, such as the temperature of the tuna.

These details are saved in the global state as a key/value pair based on the specifications of a transaction family, while the transaction processor allows Sarah's application to effectively create a transaction on the ledger. Please see the example below:

var tuna = { id: ‘0002’, holder: ‘Sarah’, location: { latitude: '15.623036831528264', longitude: '-158.466796875'}, when: '20170635123546', weight: ‘58lbs’ }

## Recording a Catch

After Sarah catches her tuna and records data for each tuna, she is able to treat a haul of tuna as a single batch of transactions. As a reminder, transaction batches are clusters of transactions that are committed to state together. Using batches, Sarah is able to record many tuna together, while still being able to specify data for each tuna. If one of the tuna transactions is invalid, the entire shipment is invalidated, that is, no tuna within the batch of tuna is validated.

## Reaching Consensus

After a batch of many transactions is submitted to the network, the network’s consensus algorithm is run to choose a node to publish the transaction block. By default, the Proof of Elapsed Time consensus algorithm is used, and the transaction validator with the shortest wait time publishes the transaction block. The transaction block is then broadcast to the publishing nodes.

Each node within the network receives the transaction block, and validators verify whether the transaction is valid or not. If the transaction is validated, the global state is updated.

Hyperledger Sawtooth is unique because of its distributed state agreement, whereby every node in the system has the same understanding of information, and, as the supply chain matures, the data stored remains consistent across the network.

With the global state adjusted, the processing plant, the regulator, and Miriam are able to see the details of the catch and who the current holder is, thus, keeping the supply chain transparent and verifiable.

## Other Actors in the Supply Chain

Before Sarah's tuna can reach Miriam's restaurant, they need to go through a tuna processing plant. Also, regulators will need to verify and view details from the ledger. Therefore, both parties will gain entry to this Sawtooth blockchain. The regulators will need to query the ledger to confirm that Sarah is legally catching her fish. At the same time, tuna processing plants will need to record their processing and shipping of the tuna on the ledger.

## Summary of Transaction Flow

Now, let's review the summary of the transaction flow:

[Summary of Transaction Flow](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/e0c503b430152897e29dec1c95ba99e2/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Sawtooth_section_3_summary_of_transaction_flow.png)

1. Sarah catches a tuna and uses the application's user interface to record all the details about the catch to the ledger. An entire haul of tuna can be treated as a transaction batch, with each individual tuna registered as a transaction within the batch.
1. After the details of the catch are saved to the ledger and the tuna is passed along the supply chain, the processing plant may use their own application to query the ledger for details about specific catches, such as weight. The processing plant will add details reflecting the processing date and time, as well as other relevant information.
1. As the tuna is passed along the supply chain, the regulator may use their respective application to query the ledger for details about specific catches, such as the owner and location of the catch, to verify legitimacy.
1. Lastly, when the haul of tuna arrives at Miriam's restaurant, Miriam is able to use her application to query the ledger, to check and make sure Sarah was truthful in her account of where each fish was sourced. This, in turn, guarantees Miriam's restaurant is serving their customers the sustainably caught fish they advertise.

## Requirements Supported by Hyperledger Sawtooth

Hyperledger Sawtooth is a blockchain framework with potential in IoT, manufacturing, finance, and enterprise. Hyperledger Sawtooth supports diverse requirements, including both permissioned and permissionless deployments, and a pluggable consensus algorithm. This framework also provides a revolutionary consensus algorithm, Proof of Elapsed Time (PoET), that allows for versatility and scalability suited for a variety of solutions.

Hyperledger Sawtooth supports many different infrastructural requirements, such as:

- Permissioned and permissionless infrastructure
- Modular blockchain architecture
- Scalability, which is good for larger blockchain networks due to higher throughput
- Many languages for transaction logic.

## Transaction Batching

Hyperledger Sawtooth transaction batches are clusters of transactions that are either all committed to state together, or none of the transactions are committed at all. As a result, transaction batches are often described as an atomic unit of change, since a group of transactions are treated as one, and are committed to the state as one. Every single transaction in Hyperledger Sawtooth is submitted within a batch. Batches can contain as little as a single transaction.

When a transaction is created by a client, the batch is submitted to the validator (which we will cover more in depth in the next section). Transactions are organized into a batch in the order they are intended to be committed. The validator then, in turn, applies each transaction within the batch, leading to a change in the global state. The batch is committed to the state. If one transaction within the batch is invalid, then none of the transactions within that batch are committed.

In summary, transaction batching allows a group of transactions to be applied in a specific order, and if any are invalid, then none of the transactions are applied. This is a powerful tool that can be utilized by many enterprise solutions, as it provides greater efficiency and control for end users.

## Validators

In any blockchain network, modifying the global state requires creating and applying a transaction. In Hyperledger Sawtooth, validators apply blocks that cause a change in the state. More specifically, validators validate transaction blocks, and ensure that transactions result in state changes that are consistent across all participants in the network.

To start, a user creates a transaction batch and submits it to a validator via a client and REST API. The validator then checks the transaction batch and applies it if it is considered valid, resulting in a change to the state. In terms of our demonstrated scenario, Sarah, the fisherman, creates a transaction batch to record information about a group of tuna catches. The validator would then apply the transactions, and the state would be updated if all appropriate attributes are present: a unique ID number, location and time of the catch, weight, and who caught the fish. If any of these elements are missing, the transactions within the batch would not be applied, and the state would not be updated.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/c7b3d5552070184b7b56fc25d316f585/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Sawtooth_validators.png)

## Journal

In Hyperledger Sawtooth, the journal maintains and extends the blockchain for the validator. It is responsible for validating candidate blocks, evaluating valid blocks to determine if they are the correct chain head, and generating new blocks to extend the chain. Transaction batches arrive at the journal, where they are evaluated, validated, and added to the blockchain. Additionally, the journal resolves forks, which occur due to disagreements over who commits a block. Once blocks are completed, they are delivered to the ChainController for validation and fork resolution.  To see how the elements of the journal interact with one another, take a look at the diagram on the next page.

Another key feature of the journal is its flexibility in allowing pluggable consensus algorithms.

## Consensus Interface

Consensus in Hyperledger Sawtooth is modular, meaning that the consensus algorithm can be easily modified. Hyperledger Sawtooth provides an abstract interface that supports both PBFT and Nakamoto-style algorithms. To implement a new consensus algorithm in Hyperledger Sawtooth, you must implement the distinct interface for: block publisher, block verifier, and fork resolution.

- Block publisher: Creates new candidate blocks to extend the chain.
- Block verifier: Verifies that candidate blocks are published in accordance with consensus rules.
- Fork resolver: Chooses which fork to use as the chain head for consensus algorithms that result in a fork.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/a6cfe922dbd88b452ce58d493273f9e4/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Consensus_interface.png)

These interfaces are used by the journal component. The journal verifies that all the dependencies for the transaction batches are satisfied. When verified, completed batches are checked for validity and fork resolution, and then, they are published within a block.

## Transaction Families

As with any blockchain framework, transaction updates need to be approved and shared between many untrusted parties. As such, many blockchain frameworks have a mechanism for supporting distributed ledgers, as well as a method for changing the state of the shared ledger.

In Hyperledger Sawtooth, the data model that captures the state and the transaction language that changes the state are implemented using transaction families.

A transaction family consists of a group of operations or transaction types that are allowed on the shared ledgers. This allows for flexibility in the level of versatility and risk that exists on a network. Transaction families are often called 'safer' smart contracts, because they specify a predefined set of acceptable smart contract templates, as opposed to programming smart contracts from scratch.

Hyperledger Sawtooth’s transaction families can be written in many languages, including Javascript, Java, C++, Python, and Go, which allows flexibility for businesses to bring their own transaction families. Hyperledger Sawtooth allows the developers to specify the address/namespace of data, which provides flexibility in defining, sharing, and reusing data between different transaction families.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/8f6a37e9af4a9e8117c7d1b779e0b405/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Transaction_families.png)

## Transaction Processors

A transaction processor provides the server-side business logic that operates on assets within a network. Hyperledger Sawtooth supports pluggable transaction processors, that are customizable based on the specific application. Businesses are able to develop transaction processors that do exactly what their applications need. Additionally, transaction processors can be written in a variety of languages (Java, Python, C, C++, JavaScript, and Go), allowing for ease of use and simplicity when handling assets.

Each node within the Hyperledger Sawtooth network runs a transaction processor. This transaction processor processes incoming transactions submitted by authorized clients. In Hyperledger Sawtooth, the Sawtooth SDK allows programmers to focus on developing application logic, as opposed to building communication mechanisms between transaction processors.

Later in this chapter, in the Writing an Application section, you will be able to explore how exactly transaction processors interact with a client and other Hyperledger Sawtooth elements.

## Sawtooth Node

Hyperledger Sawtooth organizations run a node that interacts with the Hyperledger Sawtooth network. Each node runs at least three things:

- The main validator process
- The REST service listening for requests (could be transaction posts or state queries)
- One or more transaction processors

Each organization that enters the Hyperledger Sawtooth network runs at least one node, and receives transactions submitted by fellow nodes.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/274566f591da0f1ee0ea5035f5415a7e/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Sawtooth_node.png)

## Introducing Proof of Elapsed Time (PoET)

The consensus algorithm commonly used in a Hyperledger Sawtooth network is the Proof of Elapsed Time, or PoET. PoET impartially determines who will commit a transaction to state using a lottery function that elects a leader from many different distributed nodes.

Hyperledger Sawtooth’s PoET algorithm differs from the Proof of Work algorithm implemented by the Bitcoin blockchain in that Proof of Work relies on vast amounts of power, while Proof of Elapsed Time is able to ensure trust and randomness in electing a leader, without the high power consumption. PoET allows for increased scalability and participation, as every node in the network has an equal opportunity to create the next block on the chain.

## How Proof of Elapsed Time Works

To start, each validator within the network requests a wait time from an enclave, or a trusted function. This is where the 'Elapsed Time' comes into play. The validator with the shortest wait time for a specific block is appointed the leader, and creates the block to be committed to the ledger. As a result, a truly random leader is elected, and the amount of power or type of hardware you have will not give you an advantage. Using simple functions, the network can verify that the winning validator did indeed 'win', by proving that it had the shortest time to wait before assuming the leadership position.

Proof of Elapsed Time is revolutionary in its ability to achieve distributed consensus using a lottery function. This not only allows for easy verification and fairness within the network, but also for incredible scalability. Without the heavy costs of participating in consensus, anyone can participate in the network. One of Hyperledger Sawtooth's main advantages is that it allows the size of the network to scale. That is, Hyperledger Sawtooth is nearly limitless in the network size it can support.

## Forks

While PoET provides many benefits and aids tremendously with scalability, there is a downside to the PoET consensus algorithm. And that is the issue of forks. The PoET algorithm may lead to forking, in which two 'winners' propose a block. Each fork has to be resolved by validators, and this results in a delay in reaching consistency across the network.

As stated in the Sawtooth documentation:

"Completed Blocks are delivered to the Chain controller for validation and fork resolution." - [](https://intelledger.github.io/architecture/journal.html)

## Becoming Involved with the Hyperledger Sawtooth Project

Hyperledger Sawtooth is an open source project, where ideas and code can be publicly discussed, created, and reviewed. There are many ways to join the Hyperledger Sawtooth community, and in the next few pages we are highlighting some of the ways to get involved, either from a technical standpoint, or from an ideas/issues creation perspective.

## Community Meetings and Mailing Lists

You can join the online meetings on Sawtooth Sprint planning and Tech Forums. Check the Hyperledger Community Meetings Calendar for the timing of these meetings: https://calendar.google.com/calendar/embed?src=linuxfoundation.org_nf9u64g9k9rvd9f8vp4vur23b0%40group.calendar.google.com&ctz=America/SanFrancisco.

Some of the recordings of previous virtual tech forums on Hyperledger Sawtooth can be found here: https://drive.google.com/drive/folders/0B_NJV6eJXAA1VnFUakRzaG1raXc.

You can also join the mailing list(s) for technical discussions and announcements: https://lists.hyperledger.org/mailman/listinfo/hyperledger-stl.

## GitHub and Rocket.Chat

You can also get involved with the Hyperledger Sawtooth community on GitHub and Rocket.Chat.

All code available on GitHub is forkable and viewable:

https://github.com/hyperledger/sawtooth-core
https://github.com/hyperledger/sawtooth-supply-chain.

You can also join the live conversations on Rocket.Chat (which is an alternative to Slack), using your Linux Foundation ID:

https://chat.hyperledger.org/channel/sawtooth
https://chat.hyperledger.org/channel/sawtooth-consensus
https://chat.hyperledger.org/channel/sawtooth-burrow.