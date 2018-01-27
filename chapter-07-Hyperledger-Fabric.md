# Hyperledger Fabric

## Defining Our Actors

- Sarah is the fisherman who sustainably and legally catches tuna.
- Regulators verify that the tuna has been legally and sustainably caught.
- Miriam is a restaurant owner who will serve as the end user, in this situation.
- Carl is another restaurant owner fisherman Sarah can sell tuna to.

Using Hyperledger Fabric, we will be demonstrating how tuna fishing can be improved starting from the source, fisherman Sarah, and the process by which she sells her tuna to Miriam's restaurant.

## Featured Hyperledger Fabric Elements

- Channels are data partitioning mechanisms that allow transaction visibility for stakeholders only. Each channel is an independent chain of transaction blocks containing only transactions for that particular channel.

- The chaincode (Smart Contracts) encapsulates both the asset definitions and the business logic (or transactions) for modifying those assets. Transaction invocations result in changes to the ledger.

- The ledger contains the current world state of the network and a chain of transaction invocations. A shared, permissioned ledger is an append-only system of records and serves as a single source of truth.

- The network is the collection of data processing peers that form a blockchain network. The network is responsible for maintaining a consistently replicated ledger.

- The ordering service is a collection of nodes that orders transactions into a block.

- The world state reflects the current data about all the assets in the network. This data is stored in a database for efficient access. Current supported databases are LevelDB and CouchDB.

- The membership service provider (MSP) manages identity and permissioned access for clients and peers.

## The Catch

We will start with Sarah, our licensed tuna fisher, who makes a living selling her tuna to multiple restaurants. Sarah operates as a private business, in which her company frequently makes international deals. Through a client application, Sarah is able to gain entry to a Hyperledger Fabric blockchain network comprised of other fishermen, as well as regulators and restaurant owners. Sarah has the ability to add to and update information in the blockchain network's  ledger as tuna pass through the supply chain, while regulators and restaurants have read access to the ledger.

After each catch, Sarah records information about each individual tuna, including: a unique ID number, the location and time of the catch, its weight, the vessel type, and who caught the fish. For the sake of simplicity, we will stick with these six data attributes. However, in an actual application, many more details would be recorded, from toxicology, to other physical characteristics.

These details are saved in the world state as a key/value pair based on the specifications of a chaincode contract, allowing Sarah’s application to effectively create a transaction on the ledger. You can see the example below:

`$ var tuna = { id: ‘0001’, holder: ‘Sarah’, location: { latitude: '41.40238', longitude: '2.170328'}, when: '20170630123546', weight: ‘58lbs’, vessel : ‘9548E’ }`

## The Incentives

Miriam is a restaurant owner looking to source low cost, yet high quality tuna that have been responsibly caught. Whenever Miriam buys tuna, she is always uncertain whether she can trust that the tuna she is purchasing is legally and sustainably caught, given the prominence of illegal and unreported tuna fishing.

At the same time, as a legitimate and experienced fisherman, Sarah strives to make a living selling her tuna at a reasonable price. She would also like autonomy over who she sells to and at what price.

Luckily for both Sarah and Miriam, Hyperledger Fabric can help!

## The Sale

Normally, Sarah sells her tuna to restaurateurs, such as Carl, for $80 per pound. However, Sarah agrees to give Miriam a special price of $50 per pound of tuna, rather than her usual rate. In a traditional public blockchain, once Sarah and Miriam have completed their transaction, the entire network is able to view the details of this agreement, especially the fact that Sarah gave Miriam a special price. As you can imagine, having other restaurateurs, such as Carl, aware of this deal is not economically advantageous for Sarah.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/c30530b13fd201e9d92b50dcc04b48af/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/fabric_sale_scenario.png)

## The Regulators

Regulators will also gain entry to this Hyperledger Fabric blockchain network to confirm, verify, and view details from the ledger. Their application will allow these actors to query the ledger and see the details of each of Sarah’s catches to confirm that she is legally catching her fish. Regulators only need to have query access, and do not need to add entries to the ledger. With that being said, they may be able to adjust who can gain entry to the network and/or be able to remove fishermen from the network, if found to be partaking in illegal activities.

## Gaining Network Membership

Hyperledger Fabric is a permissioned network, meaning that only participants who have been approved can gain entry to the network. To handle network membership and identity, membership service providers (MSP) manage user IDs, and authenticate all the participants in the network. A Hyperledger Fabric blockchain network can be governed by one or more MSPs. This provides modularity of membership operations, and interoperability across different membership standards and architectures.

In our scenario, the regulator, the approved fishermen, and the approved restaurateurs should be the only ones allowed to join the network. To achieve this, a membership service provider (MSP) is defined to accommodate membership for all members of this supply chain. In configuring this MSP, certificates and membership identities are created. Policies are then defined to dictate the read/write policies of a channel, or the endorsement policies of a chaincode.

Our scenario has two separate chaincodes, which are run on three separate channels. The two chaincodes are: one for the price agreement between the fisherman and the restaurateur, and one for the transfer of tuna. The three channels are: one for the price agreement between Sarah and Miriam; one for the price agreement between Sarah and Carl; and one for the transfer of tuna. Each member of this network knows about each other and their identity. The channels provide privacy and confidentiality of transactions.

In Hyperledger Fabric, MSPs also allow for dynamic membership to add or remove members to maintain integrity and operation of the supply chain. For example, if Sarah was found to be catching her fish illegally, she can have her membership revoked, without compromising the rest of the network. This feature is critical, especially for enterprise applications, where business relationships change over time.

## Summary of Demonstrated Scenario

Below is a summary of the tuna catch scenario presented in this section:

1. Sarah catches a tuna and uses the supply chain application’s user interface to record all the details about the catch to the ledger. Before it reaches the ledger, the transaction is passed to the endorsing peers on the network, where it is then endorsed. The endorsed transaction is sent to the ordering service, to be ordered into a block. This block is then sent to the committing peers in the network, where it is committed after being validated.
1. As the tuna is passed along the supply chain, regulators may use their own application to query the ledger for details about specific catches (excluding price, since they do not have access to the price-related chaincode).
1. Sarah may enter into an agreement with a restaurateur Carl, and agree on a price of $80 per pound. They use the blue channel for the chaincode contract stipulating $80/lb. The blue channel's ledger is updated with a block containing this transaction.
1. In a separate business agreement, Sarah and Miriam agree on a special price of $50 per pound. They use the red channel's chaincode contract stipulating $50/lb. The red channel's ledger is updated with a block containing this transaction.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/61bbd7eb188c20cc6428391379df45e0/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Demonstrated_Tuna_Fishing_Scenario.png)

## Roles within a Hyperledger Fabric Network

There are three different types of roles within a Hyperledger Fabric network:

- Clients

Clients are applications that act on behalf of a person to propose transactions on the network.

- Peers

Peers maintain the state of the network and a copy of the ledger. There are two different types of peers: endorsing and committing peers. However, there is an overlap between endorsing and committing peers, in that endorsing peers are a special kind of committing peers. All peers commit blocks to the distributed ledger.

- Endorsers simulate and endorse transactions
- Committers verify endorsements and validate transaction results, prior to committing transactions to the blockchain.

- Ordering Service

The ordering service accepts endorsed transactions, orders them into a block, and delivers the blocks to the committing peers.

## How to Reach Consensus

In a distributed ledger system, consensus is the process of reaching agreement on the next set of transactions to be added to the ledger. In Hyperledger Fabric, consensus is made up of three distinct steps:

- Transaction endorsement
- Ordering
- Validation and commitment.

These three steps ensure the policies of a network are upheld. We will explore how these steps are implemented by exploring the transaction flow.

## Transaction Flow (Step 1)

Within a Hyperledger Fabric network, transactions start out with client applications sending transaction proposals, or, in other words, proposing a transaction to endorsing peers.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/21431955acd5b7888ca8d393c94deaf8/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Key_Components_-_Transaction_Proposal.png)

Client applications are commonly referred to as applications or clients, and allow people to communicate with the blockchain network. Application developers can leverage the Hyperledger Fabric network through the application SDK.

## Transaction Flow (Step 2)

Each endorsing peer simulates the proposed transaction, without updating the ledger. The endorsing peers will capture the set of Read and Written data, called RW Sets. These RW sets capture what was read from the current world state while simulating the transaction, as well as what would have been written to the world state had the transaction been executed. These RW sets are then signed by the endorsing peer, and returned to the client application to be used in future steps of the transaction flow.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/13e5a6a80c0e150f46d45ec0634b86b8/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Transaction_flow_step_2.png)

Endorsing peers must hold smart contracts in order to simulate the transaction proposals.

## Transaction Endorsement

A transaction endorsement is a signed response to the results of the simulated transaction. The method of transaction endorsements depends on the endorsement policy which is specified when the chaincode is deployed. An example of an endorsement policy would be "the majority of the endorsing peers must endorse the transaction". Since an endorsement policy is specified for a specific chaincode, different channels can have different endorsement policies.

## Transaction Flow (Step 3)

The application then submits the endorsed transaction and the RW sets to the ordering service. Ordering happens across the network, in parallel with endorsed transactions and RW sets submitted by other applications.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/b6e7b13624d1cff4152e2c223538c355/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Transaction_flow_step_3.png)

## Transaction Flow (Step 4)

The ordering service takes the endorsed transactions and RW sets, orders this information into a block, and delivers the block to all committing peers.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/eeb54ce57f8a6018443e22f34b3ebad9/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Transaction_Flow_Step_4.png)

The ordering service, which is made up of a cluster of orderers, does not process transactions, smart contracts, or maintains the shared ledger. The ordering service accepts the endorsed transactions and specifies the order in which those transactions will be committed to the ledger. The Fabric v1.0 architecture has been designed such that the specific implementation of 'ordering' (Solo, Kafka, BFT) becomes a pluggable component. The default ordering service for Hyperledger Fabric is Kafka. Therefore, the ordering service is a modular component of Hyperledger Fabric.

## Ordering (Part I)

Transactions within a timeframe are sorted into a block and are committed in sequential order.

In a blockchain network, transactions have to be written to the shared ledger in a consistent order. The order of transactions has to be established to ensure that the updates to the world state are valid when they are committed to the network. Unlike the Bitcoin blockchain, where ordering occurs through the solving of a cryptographic puzzle, or mining, Hyperledger Fabric allows the organizations running the network to choose the ordering mechanism that best suits that network. This modularity and flexibility makes Hyperledger Fabric incredibly advantageous for enterprise applications.

## Ordering (Part II)

Hyperledger Fabric provides three ordering mechanisms: SOLO, Kafka, and Simplified Byzantine Fault Tolerance (SBFT), the latter of which has not yet been implemented in Fabric v1.0.

- SOLO is the Hyperledger Fabric ordering mechanism most typically used by developers experimenting with Hyperledger Fabric networks. SOLO involves a single ordering node.

- Kafka is the Hyperledger Fabric ordering mechanism that is recommended for production use. This ordering mechanism utilizes Apache Kafka, an open source stream processing platform that provides a unified, high-throughput, low-latency platform for handling real-time data feeds. In this case, the data consists of endorsed transactions and RW sets. The Kafka mechanism provides a crash fault-tolerant solution to ordering.

- SBFT stands for Simplified Byzantine Fault Tolerance. This ordering mechanism is both crash fault-tolerant and byzantine fault-tolerant, meaning that it can reach agreement even in the presence of malicious or faulty nodes. The Hyperledger Fabric community has not yet implemented this mechanism, but it is on their roadmap.

These three ordering mechanisms provide alternate methodologies for agreeing on the order of transactions.

## Transaction Flow (Step 5)

The committing peer validates the transaction by checking to make sure that the RW sets still match the current world state. Specifically, that the Read data that existed when the endorsers simulated the transaction is identical to the current world state. When the committing peer validates the transaction, the transaction is written to the ledger, and the world state is updated with the Write data from the RW Set.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/b05e5430900cf5e414e307d2f99de088/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Transaction_Flow_Step_5.png)

If the transaction fails, that is, if the committing peer finds that the RW set does not match the current world state, the transaction ordered into a block will still be included in that block, but it will be marked as invalid, and the world state will not be updated.

Committing peers are responsible for adding blocks of transactions to the shared ledger and updating the world state. They may hold smart contracts, but it is not a requirement.

## Transaction Flow (Step 6)

Lastly, the committing peers asynchronously notify the client application of the success or failure of the transaction. Applications will be notified by each committing peer.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/ba380b73a55eff97c85da3abdc1d86e8/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Transaction_Flow_Step_6.png)

## Identity Verification

In addition to the multitude of endorsement, validity, and versioning checks that take place, there are also ongoing identity verifications happening during each step of the transaction flow. Access control lists are implemented on the hierarchical layers of the network (from the ordering service down to channels), and payloads are repeatedly signed, verified, and authenticated as a transaction proposal passes through the different architectural components.

## Transaction Flow Summary

It is important to note that the state of the network is maintained by peers, and not by the ordering service or the client. Normally, you will design your system such that different machines in the network play different roles. That is, machines that are part of the ordering service should not be set up to also endorse or commit transactions, and vice versa. However, there is an overlap between endorsing and committing peers on the system. Endorsing peers must have access to and hold smart contracts, in addition to fulfilling the role of a committing peer. Endorsing peers do commit blocks, but committing peers do not endorse transactions.

Endorsing peers verify the client signature, and execute a chaincode function to simulate the transaction. The output is the chaincode results, a set of key/value versions that were read in the chaincode (Read set), and the set of keys/values that were written by the chaincode. The proposal response gets sent back to the client, along with an endorsement signature. These proposal responses are sent to the orderer to be ordered. The orderer then orders the transactions into a block, which it forwards to the endorsing and committing peers. The RW sets are used to verify that the transactions are still valid before the content of the ledger and world state is updated. Finally, the peers asynchronously notify the client application of the success or failure of the transaction.

## Channels

Channels allow organizations to utilize the same network, while maintaining separation between multiple blockchains. Only the members of the channel on which the transaction was performed can see the specifics of the transaction. In other words, channels partition the network in order to allow transaction visibility for stakeholders only. This mechanism works by delegating transactions to different ledgers. Only the members of the channel are involved in consensus, while other members of the network do not see the transactions on the channel.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/b23a6aaaa627620a0ab161c556ff87b3/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Key_Components_Channels.png)

The diagram above shows three distinct channels -- blue, orange, and grey. Each channel has its own application, ledger, and peers.

Peers can belong to multiple networks or channels. Peers that do participate in multiple channels simulate and commit transactions to different ledgers. The ordering service is the same across any network or channel.

A few things to remember:

- The network setup allows for the creation of channels.
- The same chaincode logic can be applied to multiple channels.
- A given user can participate in multiple channels.

## State Database

The current state data represents the latest values for all assets in the ledger. Since the current state represents all the committed transactions on the channel, it is sometimes referred to as world state.

Chaincode invocations execute transactions against the current state data. To make these chaincode interactions extremely efficient, the latest key/value pairs for each asset are stored in a state database. The state database is simply an indexed view into the chain’s committed transactions. It can therefore be regenerated from the chain at any time. The state database will automatically get recovered (or generated, if needed) upon peer startup, before new transactions are accepted. The default state database, LevelDB, can be replaced with CouchDB.

- LevelDB is the default key/value state database for Hyperledger Fabric, and simply stores key/value pairs.
- CouchDB is an alternative to LevelDB. Unlike LevelDB, CouchDB stores JSON objects. CouchDB is unique in that it supports keyed, composite, key range, and full data-rich queries.

Hyperledger Fabric’s LevelDB and CouchDB are very similar in their structure and function. Both LevelDB and CouchDB support core chaincode operations, such as getting and setting key assets, and querying based on these keys. With both, keys can be queried by range, and composite keys can be modeled to enable equivalence queries against multiple parameters. But, as a JSON document store, CouchDB additionally enables rich query against the chaincode data, when chaincode values (e.g. assets) are modeled as JSON data.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/9fa87a2726077cff05169f85584224ac/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/State_Database.png)

## Smart Contracts

As a reminder, smart contracts are computer programs that contain logic to execute transactions and modify the state of the assets stored within the ledger. Hyperledger Fabric smart contracts are called chaincode and are written in Go. The chaincode serves as the business logic for a Hyperledger Fabric network, in that the chaincode directs how you manipulate assets within the network. We will discuss more about chaincode in the Understanding Chaincode section.

## Membership Service Provider (MSP)

The membership service provider, or MSP, is a component that defines the rules in which identities are validated, authenticated, and allowed access to a network. The MSP manages user IDs and authenticates clients who want to join the network. This includes providing credentials for these clients to propose transactions. The MSP makes use of a Certificate Authority, which is a pluggable interface that verifies and revokes user certificates upon confirmed identity. The default interface used for the MSP is the Fabric-CA API, however, organizations can implement an External Certificate Authority of their choice. This is another feature of Hyperledger Fabric that is modular. Hyperledger Fabric supports many credential architectures, which allows for many types of External Certificate Authority interfaces to be used. As a result, a single Hyperledger Fabric network can be controlled by multiple MSPs, where each organization brings their favorite.

## What Does the MSP Do?

To start, users are authenticated using a certificate authority. The certificate authority identifies the application, peer, endorser, and orderer identities, and verifies these credentials. A signature is generated through the use of a Signing Algorithm and a Signature Verification Algorithm.

Specifically, generating a signature starts with a Signing Algorithm, which utilizes the credentials of the entities associated with their respective identities, and outputs an endorsement. A signature is generated, which is a byte array that is bound to a specific identity. Next, the Signature Verification Algorithm takes the identity, endorsement, and signature as inputs, and outputs 'accept' if the signature byte array corresponds with a valid signature for the inputted endorsement, or outputs 'reject' if not. If the output is 'accept', the user can see the transactions in the network and perform transactions with other actors in the network. If the output is 'reject', the user has not been properly authenticated, and is not able to submit transactions to the network, or view any previous transactions.

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/2fe3f7dc2fa52699a96ef7948432113b/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/The_role_of_membership_service_provider.jpg)

## Fabric-Certificate Authority

In general, Certificate Authorities manage enrollment certificates for a permissioned blockchain. Fabric-CA is the default certificate authority for Hyperledger Fabric, and handles the registration of user identities. The Fabric-CA certificate authority is in charge of issuing and revoking Enrollment Certificates (E-Certs). The current implementation of Fabric-CA only issues E-Certs, which supply long term identity certificates. E-Certs, which are issued by the Enrollment Certificate Authority (E-CA), assign peers their identity and give them permission to join the network and submit transactions.

## Technical Prerequisites

In order to successfully install Hyperledger Fabric, you should be familiar with Go and Node.js programming languages, and have the following features installed on your computer: cURL, Node.js, npm package manager, Go language, Docker, and Docker Compose.

If you need further details on these prerequisites, visit Chapter 4, Technical Requirements.

## Installing Hyperledger Fabric Docker Images and Binaries

Next, we will download the latest released Docker images for Hyperledger Fabric, and tag them with the latest tag. Execute the command from within the directory into which you will extract the platform-specific binaries:

`$ curl -sSL https://goo.gl/6wtTN5 | bash -s 1.1.0-alpha`

Note: Check https://hyperledger-fabric.readthedocs.io/en/latest/samples.html#binaries for the latest URL (the blue portion in the above curl command) to pull in binaries.

This command downloads binaries for cryptogen, configtxgen, configxlator, peer AND downloads the Hyperledger Fabric Docker images. These assets are placed in a bin subdirectory of the current working directory.

To confirm and see the list of Docker images you’ve just downloaded, run:

`$ docker images`

The expected response is:

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/ca726400444f52edbc3e54278077f8dd/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Fabric_installation_1.jpg)

Note the tags for each of the repositories above boxed in red. If the Docker images are not already tagged with the latest tag, perform the following command for each of the Docker images:

`$ docker tag hyperledger/fabric-tools:x86_64-1.0.2 hyperledger/fabric-tools:latest`

Swap out the blue portion with the tags you see in your list of repositories. Also, swap out the red portion with the name of the Docker image you are switching the tag for (e.g.: fabric-tools, fabric-ccenv, fabric-orderer, etc.). Repeat this step for all Docker images you see in the list.

In the screenshot above, the Docker images are already tagged. If this is the case for you, you do not need to do this extra step.

## Installing Hyperledger Fabric

As an additional measure, you may want to add the bin subdirectory to your PATH environment variable, so these can be picked up without needing to qualify the PATH to each binary. You can do this by running the following:

`$ export PATH=$PWD/bin:$PATH`

To install the Hyperledger Fabric sample code which will be used in the tutorials, do:

`$ git clone https://github.com/hyperledger/fabric-samples.git`

`$ cd fabric-samples/first-network`

## Starting a Test Hyperledger Fabric Network

Now that we have successfully installed Hyperledger Fabric, we can walk through setting up a simple network that has two members. To refer back to our demonstrated scenario, the network includes asset management of each tuna verified, transferred, and purchased between Sarah, the fisherman, and Miriam, the restaurateur. We’ll create a simple two member network consisting of two organizations (effectively, Sarah and Miriam), each maintaining two peers and an ordering service.

We will use Docker images to bootstrap our first Hyperledger Fabric network. It will also launch a container to run a scripted execution that will join peers to a channel, deploy, and instantiate the chaincode, and execute transactions against the chaincode.

## Getting Started with Your First Network

Are you ready to get started? Run this command ( within the first-network folder ):

`$ ./byfn.sh -m generate`

A brief description will appear, along with a Y/N command line prompt. Respond with a Y <Enter> to continue.

This step generates all of the certificates and keys for all our various network entities, including the genesis block used to bootstrap the ordering service and a collection of configuration transactions required to create a channel.

Next, you can start the network with the following command:

`$ ./byfn.sh -m up`

Another command line will appear, reply with Y <Enter> to continue.

Logs will appear in the command line, showing containers being launched, channels being created and joined, chaincode being installed, instantiated, and invoked on all the peers, as well as various transaction logs.

Troubleshooting Note:
If you have difficulties with the two previous commands and you suspect that your Docker images may be at fault, you can start back from scratch, which will delete and untag the Docker images.

`$ docker rmi -f $(docker images -q)`

Once you run this command, return to the Installing Hyperledger Fabric Docker Images and Binaries page, at the beginning of this section.

## Finishing Up and Shutting Down the Network

Finally, let’s test bringing down this network.

Within the same terminal, do Control+C to exit the current execution.

Then, run the following command:

`$ ./byfn.sh -m down`

Another command line will appear, reply with Y <Enter> to continue.

This command will kill your containers, remove the crypto material and four artifacts, and delete the chaincode images from your Docker Registry.

And that’s it for a simple demonstration!

These simple steps show how we can easily spin up and bring down a Hyperledger Fabric network, given the code we have. In the next section, we will learn more about chaincode.

## Chaincode

In Hyperledger Fabric, chaincode is the 'smart contract' that runs on the peers and creates transactions. More broadly, it enables users to create transactions in the Hyperledger Fabric network's shared ledger and update the world state of the assets.

Chaincode is programmable code, written in Go, and instantiated on a channel. Developers use chaincode to develop business contracts, asset definitions, and collectively-managed decentralized applications. The chaincode manages the ledger state through transactions invoked by applications. Assets are created and updated by a specific chaincode, and cannot be accessed by another chaincode.

Applications interact with the blockchain ledger through the chaincode. Therefore, the chaincode needs to be installed on every peer that will endorse a transaction and instantiated on the channel.

There are two ways to develop smart contracts with Hyperledger Fabric:

- Code individual contracts into standalone instances of chaincode
- (More efficient way) Use chaincode to create decentralized applications that manage the lifecycle of one or multiple types of business contracts, and let the end users instantiate instances of contracts within these applications.

## Chaincode Key APIs

An important interface that you can use when writing your chaincode is defined by Hyperledger Fabric - ChaincodeStub and ChaincodeStubInterface. The ChaincodeStub provides functions that allow you to interact with the underlying ledger to query, update, and delete assets. The key APIs for chaincode include:

`func (stub *ChaincodeStub) GetState(key string) ([]byte, error)`
Returns the value of the specified key from the ledger. Note that GetState doesn't read data from the Write set, which has not been committed to the ledger. In other words, GetState doesn't consider data modified by PutState that has not been committed. If the key does not exist in the state database, (nil, nil) is returned.

`func (stub *ChaincodeStub) PutState(key string, value []byte) error`
Puts the specified key and value into the transaction's Write set as a data-write proposal. PutState doesn't affect the ledger until the transaction is validated and successfully committed.

`func (stub *ChaincodeStub) DelState(key string) error`
Records the specified key to be deleted in the Write set of the transaction proposal. The key and its value will be deleted from the ledger when the transaction is validated and successfully committed.

## Overview of a Chaincode Program

When creating a chaincode, there are two methods that you will need to implement:

- Init
Called when a chaincode receives an instantiate or upgrade transaction. This is where you will initialize any application state.

- Invoke
Called when the invoke transaction is received to process any transaction proposals.

As a developer, you must create both an Init and an Invoke method within your chaincode. The chaincode must be installed using the `peer chaincode install` command, and instantiated using the `peer chaincode instantiate` command before the chaincode can be invoked. Then, transactions can be created using the `peer chaincode invoke` or `peer chaincode query` commands.

## Sample Chaincode Decomposed - Dependencies

Let’s now walk through a sample chaincode written in Go, piece by piece:

```go
package main

import (
  "fmt"
  "github.com/hyperledger/fabric/core/chaincode/shim"
  "github.com/hyperledger/fabric/protos/peer"
)
```

The `import` statement lists a few dependencies that you will need for your chaincode to build successfully.

fmt - contains Println for debugging/logging
github.com/hyperledger/fabric/core/chaincode/shim - contains the definition for the chaincode interface and the chaincode stub, which you will need to interact with the ledger, as we described in the Chaincode Key APIs section
github.com/hyperledger/fabric/protos/peer - contains the peer protobuf package.

## Sample Chaincode Decomposed - Struct

```go
type SampleChaincode struct {

}
```

This might not look like much, but this is the statement that begins the definition of an object/class in Go. SampleChaincode implements a simple chaincode to manage an asset.

## Sample Chaincode Decomposed - Init Method

Next, we’ll implement the Init method. Init is called during the chaincode instantiation to initialize data required by the application. In our sample, we will create the initial key/value pair for an asset, as specified on the command line:

```go
func (t *SampleChaincode) Init(stub shim.ChainCodeStubInterface) peer.Response {

  // Get the args from the transaction proposal
  args := stub.GetStringArgs()

  if len(args) != 2 {
    return shim.Error("Incorrect arguments. Expecting a key and a value")
  }

  // We store the key and the value on the ledger
  err := stub.PutState(args[0], []byte(args[1]))

  if err != nil {
    return shim.Error(fmt.Sprintf("Failed to create asset: %s", args[0]))
  }

  return shim.Success(nil)
}
```

The Init implementation accepts two parameters as inputs, and proposes to write a key/value pair to the ledger by using the stub.PutState function. GetStringArgs retrieves and checks the validity of arguments which we expect to be a key/value pair. Therefore, we check to ensure that there are two arguments specified. If not, we return an error from the Init method, to indicate that something went wrong. Once we have verified the correct number of arguments, we can store the initial state in the ledger. In order to accomplish this, we call the stub.PutState function, specifying the first argument as the key, and the second argument as the value for that key. If no errors are returned, we will return success from the Init method.

## Sample Chaincode Decomposed - Invoke Method

Now, we’ll explore the Invoke method, which gets called when a transaction is proposed by a client application. In our sample, we will either get the value for a given asset, or propose to update the value for a specific asset.

```go
func (t *SampleChaincode) Invoke(stub shim.ChaincodeStubInterface) peer.Response {

  // Extract the function and args from the transaction proposal
  fn, args := stub.GetFunctionAndParameters()

  var result string

  var err error

  if fn == "set" {
    result, err = set(stub, args)
  } else { // assume 'get' even if fn is nil
    result, err = get(stub, args)
  }

  if err != nil { //Failed to get function and/or arguments from transaction proposal
    return shim.Error(err.Error())
  }

  // Return the result as success payload
  return shim.Success([]byte(result))
}
```

There are two basic actions a client can invoke: get and set.

The get method will be used to query and return the value of an existing asset.
The set method will be used to create a new asset or update the value of an existing asset.
To start, we’ll call GetFunctionandParameters to isolate the function name and parameter variables. Each transaction is either a set or a get. Let's first look at how the set method is implemented:

```go
func set(stub shim.ChaincodeStubInterface, args []string) (string, error) {

  if len(args) != 2 {
    return "", fmt.Errorf("Incorrect arguments. Expecting a key and a value")
  }

  err := stub.PutState(args[0], []byte(args[1]))

  if err != nil {
    return "", fmt.Errorf("Failed to set asset: %s", args[0])
  }

  return args[1], nil
}
```

The set method will create or modify an asset identified by a key with the specified value. The set method will modify the world state to include the key/value pair specified. If the key exists, it will override the value with the new one, using the PutState method; otherwise, a new asset will be created with the specified value.

Next, let's look at how the get method is implemented:

```go
func get(stub shim.ChaincodeStubInterface, args []string) (string, error) {

  if len(args) != 1 {
    return "", fmt.Errorf("Incorrect arguments. Expecting a key")
  }

  value, err := stub.GetState(args[0])

  if err != nil {
    return "", fmt.Errorf("Failed to get asset: %s with error: %s", args[0], err)
  }

  if value == nil {
    return "", fmt.Errorf("Asset not found: %s", args[0])
  }

  return string(value), nil
}
```

The get method will attempt to retrieve the value for the specified key. If the application does not pass in a single key, an error will be returned; otherwise, the GetState method will be used to query the world state for the specified key. If the key has not yet been added to the ledger (and world state), then an error will be returned; otherwise, the value that was set for the specified key is returned from the method.

## Sample Chaincode Decomposed - Main Function

The last piece of code in this sample is the main function, which will call the Start function. The main function starts the chaincode in the container during instantiation.

```go
func main() {

  err := shim.Start(new(SampleChaincode))

  if err != nil {
    fmt.Println("Could not start SampleChaincode")
  } else {
    fmt.Println("SampleChaincode successfully started")
  }
}
```