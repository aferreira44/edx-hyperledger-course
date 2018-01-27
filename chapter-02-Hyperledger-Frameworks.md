# Hyperledger Frameworks

## Components of Hyperledger Frameworks

Hyperledger business blockchain frameworks are used to build enterprise blockchains for a consortium of organizations. They are different than public ledgers like the Bitcoin blockchain and Ethereum. The Hyperledger frameworks include:

An append-only distributed ledger
A consensus algorithm for agreeing to changes in the ledger
Privacy of transactions through permissioned access
Smart contracts to process transaction requests.

[Components of Hyperledger Frameworks](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/0747265232da64643d21679294cbbe19/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/Components_of_blockchain.jpg)

## Hyperledger Iroha v0.95

[Hyperledger Iroha](https://hyperledger.org/projects/iroha) is a blockchain framework contributed by Soramitsu, Hitachi, NTT Data, and Colu. Hyperledger Iroha is designed to be simple and easy to incorporate into infrastructure projects requiring distributed ledger technology. Hyperledger Iroha emphasizes mobile application development with client libraries for Android and iOS, making it distinct from other Hyperledger frameworks. Inspired by Hyperledger Fabric, Hyperledger Iroha seeks to complement Hyperledger Fabric and Hyperledger Sawtooth, while providing a development environment for C++ developers to contribute to Hyperledger.

In conclusion, Hyperledger Iroha features a simple construction, modern, domain-driven C++ design, along with the consensus algorithm [YAC](https://www.overleaf.com/read/wzhwjzbjvrzn#/40115559/).

## Hyperledger Sawtooth v0.8

[Hyperledger Sawtooth](https://www.hyperledger.org/projects/sawtooth), contributed by Intel, is a blockchain framework that utilizes a modular platform for building, deploying, and running distributed ledgers. Distributed ledger solutions built with Hyperledger Sawtooth can utilize various consensus algorithms based on the size of the network. By default, it uses the Proof of Elapsed Time (PoET) consensus algorithm, which provides the scalability of the Bitcoin blockchain without the high energy consumption. PoET allows for a highly scalable network of validator nodes. Hyperledger Sawtooth is designed for versatility, with support for both permissioned and permissionless deployments.

## Hyperledger Fabric v1.0

[Hyperledger Fabric](https://www.hyperledger.org/projects/fabric) was the first proposal for a codebase, combining previous work done by Digital Asset Holdings, Blockstream's libconsensus, and IBM's OpenBlockchain. Hyperledger Fabric provides a modular architecture, which allows components such as consensus and membership services to be plug-and-play. Hyperledger Fabric is revolutionary in allowing entities to conduct confidential transactions without passing information through a central authority. This is accomplished through different channels that run within the network, as well as the division of labor that characterizes the different nodes within the network. Lastly, it is important to remember that, unlike Bitcoin, which is a public chain, Hyperledger Fabric supports permissioned deployments.

"If you have a large blockchain network and you want to share data with only certain parties, you can create a private channel with just those participants. It is the most distinctive thing about Fabric right now."

- Brian Behlendorf, Executive Director of Hyperledger, The Linux Foundation

## Hyperledger Indy

[Hyperledger Indy](https://www.hyperledger.org/projects) is a distributed ledger purpose-built for decentralized identity. Hyperledger Indy's goal is to achieve this by developing a set of

"(...) decentralized identity specs and artifacts that are independent of any particular ledger and will enable interoperability across any DLT that supports them."

Contributed by the Sovrin Foundation, Hyperledger Indy allows individuals to manage and control their digital identities. Rather than having businesses store huge amounts of personal data of individuals, Hyperledger Indy allows businesses to store pointers to identity. Once the company verifies the other party's identity, it throws it away.

According to Brian Behlendorf,

"(...) identity is a toxic asset that could present a liability to organizations."

Indeed, since 2013, over 9 billion data records were lost or stolen. What is striking is that, out of these, only 4% were encrypted, and hence, rendered useless after being stolen (also called 'secure breaches'). You can find detailed statistics at http://breachlevelindex.com/.

One of the key principles of Hyperledger Indy is its 'Privacy by Design' approach. Given the immutable nature of the DLT, it is all the more important that digital identities be handled with the utmost care, keeping human values front and center.

"Hyperledger Indy lets users authenticate identity based on the attributes they are willing to store and share themselves. This can reduce the amount of liability contained within a business because the data can be kept with the user and presented to you again in a way that you can trust and validate that what has been said really was said and is trusted by the other parties you do business with."

- Nathan George, Maintainer, Hyperledger Indy

## Hyperledger Burrow v0.16.1

Formally known as eris-db, [Hyperledger Burrow](https://www.hyperledger.org/projects/hyperledger-burrow) was released in December 2014. Currently under incubation, Hyperledger Burrow is a permissionable smart contract machine that provides a modular blockchain client with a permissioned smart contract interpreter built- in part to the specification of the Ethereum Virtual Machine (EVM). It is the only available Apache-licensed EVM implementation.

Following are the major components of Burrow:

- The Gateway provides interfaces for systems integration and user interfaces
- The Smart contract application engine facilitates integration of complex business logic
- The Consensus Engine serves the dual purpose of: 
        - a. Maintaining the networking stack between the nodes, and,
        - b. Ordering transactions
- The Application Blockchain Interface (ABCI) provides interface specification for the consensus engine and smart contract application engine to connect.

You can learn more about Hyperledger Burrow at [https://monax.io/platform/db/](https://monax.io/platform/db/).