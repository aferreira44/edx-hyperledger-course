# README

## Technical Prerequisites

In order to successfully install Hyperledger Sawtooth, you should be familiar with Go and Node.js programming languages, and have the following features installed on your computer: cURL, Node.js, npm package manager, Go language, Docker, and Docker Compose.

If you need further details on these prerequisites, visit Chapter 4, Technical Requirements.

## Installing Hyperledger Sawtooth

Hyperledger Sawtooth is a suite that permits the creation and utilization of a distributed ledger. Installing Hyperledger Sawtooth will involve adding signing keys for the software creator to our environment, including the repository that contains the code to our system, and performing a typical update/install.

Hyperledger Sawtooth validators can be run either from pre-built Docker containers, or natively, using Ubuntu 16.04. In this tutorial, we will demonstrate how to set up Hyperledger Sawtooth using Docker.

Our simple Sawtooth environment will include a single validator using the dev-mode consensus, a REST API connected to the validator, transaction processors, and a client container.

Download the following Docker Compose file as sawtooth-default.yaml at [](https://raw.githubusercontent.com/hyperledger/education/master/LFS171x/sawtooth-material/sawtooth-default.yaml).

## Starting Hyperledger Sawtooth

We will start by opening a terminal window.

You should change your working directory to the same directory where the sawtooth-default.yaml Docker Compose file is saved.

Note: Make sure you do not have anything else running on port 8080 or port 4004.

Run the following command:

`$ docker-compose -f sawtooth-default.yaml up`

This command will download the Docker images that comprise the Hyperledger Sawtooth demo environment. The download will take several minutes. The terminal will start to display containers registering and creating initial blocks.

Make sure to have Docker running on your device before running the commands in this section. Otherwise, you will get a similar error to the one below:

ERROR: Couldn't connect to Docker daemon. You might need to start Docker for Mac.

## Logging into the Client Container

The client container is used to run Sawtooth CLI commands, which is the usual way to interact with validators or validator networks at this time.

Open a new terminal window and navigate to the same directory mentioned in this section.

Log into the client container by running the following command:

`$ docker exec -it sawtooth-client-default bash`

In your terminal, you will see something similar to the following:

root@75b380886502:/#

Your environment is now set up and you are ready to start experimenting with the network. But first, let’s confirm that our validator is up and running, and reachable from the client container. To do this, run the following command:

`$ curl http://rest-api:8080/blocks`

After running this command, you should see a json object response with “data”, array of batches, header, etc.

And, to check the connectivity from the host computer, run the following command in a new terminal window (it does not need to be the same directory as mentioned previously in this section):

`$ curl http://localhost:8080/blocks`

After running this command, you should see a json object response with “data”, array of batches, header, etc.

## Stopping Hyperledger Sawtooth

First, press Ctrl+C from the window where you originally ran docker-compose.

Then, in the terminal, you will see containers stopping. After that, run the following command:

`$ docker-compose -f sawtooth-default.yaml down`

## Applications

In a blockchain application, the blockchain will store the state of the system, in addition to the immutable record of transactions that created that state. A client application will be used to send transactions to the blockchain. The smart contracts will encode some (if not all) of the business logic.

## Designing an Application Using the Javascript SDK

We will be looking at a sample blockchain application that interfaces with Hyperledger Sawtooth. This application was written by Zac Delventhal, a maintainer on Hyperledger Sawtooth, and was originally presented at Midwest JS 2017. This example is meant to introduce you to writing an application that interfaces with Hyperledger Sawtooth, as opposed to creating a complete production implementation.

Hyperledger Sawtooth offers an SDK to abstract away many of the complicated aspects of blockchain technology. SDKs are available in multiple languages, including Java, Python, and Javascript. In this example, we will be working with the Javascript SDK. We will be examining a web client and transaction processor putting our demonstrated scenario into action.

## Review of Hyperledger Sawtooth Components

- Transaction validators validate transactions.

- Transaction families consist of "a group of operations or transaction types" (Dan Middleton) that are allowed on the shared ledger. Transaction families consist of both transaction processors (the server-side logic) and clients (for use from Web or mobile applications).

- The transaction processor provides the server-side business logic that operates on assets within a network.

- Transaction batches are clusters of transactions that are either all committed to state, or are all not committed to state.

- The network layer is responsible for communicating between validators in a Hyperledger Sawtooth network, including performing initial connectivity, peer discovery, and message handling.

- The global state contains the current state of the ledger and a chain of transaction invocations. The state for all transaction families is represented on each validator. The state is split into namespaces, which allow flexibility for transaction family authors to define, share, and reuse global state data between transaction processors.

## Sawtooth Tuna Application

Let’s get our feet wet with an example of a simple Hyperledger Sawtooth blockchain application, written in JavaScript, that relates to the tuna fish supply scenario we discussed in our demonstrated scenario. The Sawtooth Tuna Chain allows a user to create named assets (tuna fish), and transfer them between different holders designated by a public key.

In our example, we will look at:

A transaction processor
A simple browser-based client.
The transaction processor interfaces with a Sawtooth validator, and handles the validation of transactions.

The client is a simple browser-based user interface, and will allow a user to manage public/private key pairs, and submit transactions using the Sawtooth REST API.

Just in case you have not done so, clone the educational repository for this course with the Sawtooth Tuna Chain application code we have provided. Navigate in your terminal window to your projects folder or desktop.

`$ git clone https://github.com/hyperledger/education.git`

`$ cd education`

`$ cd LFS171x`

`$ cd sawtooth-material`

## File Structure of Application

Here you can see the file structure of the Sawtooth application:

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/d99202fc5d73b815887148f17dc52af4/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/File_Structure_of_Sawtooth_Application.png)

## Installation

Make sure you have Docker running on your machine before you run the next command. If you do not have Docker installed, you should review Chapter 4, Technical Requirements.

Note: Make sure you are in the sawtooth-material folder

We will use the provided docker-compose file to spin up some default Sawtooth components, including a validator and a REST API. Run the following command to start Sawtooth up:

`$ docker-compose -f sawtooth-default.yaml up`

Note: If you are getting an error, you may need to run the following instead:

`$ docker-compose -force sawtooth-default.yaml up`

Let’s run the following commands to install dependencies for the transaction processor:

`$ cd sawtooth-tuna`
`$ cd processor`
`$ npm install`

Then, we will navigate to the client folder, and run these commands to install dependencies for and build the client:

`$ cd ..`
`$ cd client`
`$ npm install`
`$ npm run build`

`$ cd ..`

Note: Make sure you are in the sawtooth-tuna folder.

## Transaction Processor

To review, there are two main components of a transaction processor: a processor class and a handler class. The Javascript SDK offers a general-purpose processor class. The handler class is customized to the application, and holds the business logic for transactions. Usually, there is one transaction processor per use case.

Make sure you are in the sawtooth-tuna folder.

In a new terminal window, start up the transaction processor by running the following:

`$ cd processor`
`$ npm start`

## Browser Client

Start the client simply by opening ../client/index.html in any browser window of your choice. One way of doing so is simply to open up the education folder and navigate to sawtooth-tuna. Click on the client folder and drag the index.html folder into a browser window.

## Creating a User

We are now ready to test out our application through the user interface. We have four options:

- Create a user within the supply chain
- Create a record of a tuna catch
- Transfer a tuna
- Accept or reject a transfer.

The application logic is contained mainly within the handlers.js file within the processor folder.

Users are just public/private key pairs stored in localStorage.

```js
makePrivateKey: () => {

let privateKey

do privateKey = randomBytes(32)

while (!secp256k1.privateKeyVerify(privateKey))

return privateKey.toString('hex')

}
```

This function creates a random 256-bit private key represented as a 64-char hex string on the client side. This should not be shared with anyone else.

```js
getPublicKey: privateKey => {

const privateBuffer = _decodeHex(privateKey)

const publicKey = secp256k1.publicKeyCreate(privateBuffer)

return publicKey.toString('hex')

}
```

This function returns the public key derived from the 256-bit private key created above. This is the key that is safe to share. It takes in the 256-bit private key and returns the public key as a hex string.

These two keys are stored together in the browser’s localStorage. If you do Inspect Element and navigate to the Application tab, under localStorage, you can view the key pairs.

** Note: This method is not the way this would be done in a production application. **

Within the user interface, you can create these keys from the Select Holder dropdown. You can use this same dropdown to switch between multiple users in localStorage.

## Creating a Record of Tuna

```js
const createAsset = (asset, owner, state) => {

const address = getAssetAddress(asset)

return state.get([address])

.then(entries => {

const entry = entries[address]

if (entry && entry.length > 0) {

throw new InvalidTransaction('Asset name in use')

}

return state.set({

[address]: encode({name: asset, owner})

})

})

}

const getAddress = (key, length = 64) => {

return createHash('sha512').update(key).digest('hex').slice(0, length)

}

const getAssetAddress = name => PREFIX + '00' + getAddress(name, 62)
```

The createAsset function adds a new asset to the state by taking in an asset name, owner as the public key, and state. Once an asset address for a specific tuna is created with the sha512 hash, the state is set to state.set({ [address]: encode({name: asset, owner: owner}) }).

Within the user interface, select the owner of the tuna in the Select Holder dropdown, then provide a unique name for the tuna in the Create Tuna Record text box. Lastly, click the Create button.

After doing this, you will see the tuna show up in the Tuna List, along with its associated owner.

## Transferring a Tuna

```js
const transferAsset = (asset, owner, signer, state) => {

const address = getTransferAddress(asset)

const assetAddress = getAssetAddress(asset)

return state.get([assetAddress])

.then(entries => {

const entry = entries[assetAddress]

if (!entry || entry.length === 0) {

throw new InvalidTransaction]('Asset does not exist')

}

if (signer !== decode(entry).owner) {

throw new InvalidTransaction('Only an Asset\'s owner may transfer it')

}

return state.set({

[address]: encode({name: asset, owner: owner})

})

})

}
```

The transferAsset function proposes a transfer of ownership for a particular asset to the state by taking in the asset name, owner to transfer to, signer (current owner) and state. If all the checks pass, the state is updated with the proposed transfer [address]: encode({asset, owner}).

Any tuna assigned to a particular user can be transferred to another owner (public key) using the dropdowns under Transfer Tuna. Note that the transfer must be accepted by that user before it is finalized.

In the above screenshot, we are proposing to transfer the ownership of tuna4 from the current owner (identified by the key starting with 02) to a new owner (identified by the key starting with 03).

## Accepting or Rejecting Transfers (Part I)

```js
const acceptTransfer = (asset, signer, state) => {

const address = getTransferAddress(asset)

return state.get([address])

.then(entries => {

const entry = entries[address]

if (!entry || entry.length === 0) {

throw new InvalidTransaction('Asset is not being transfered')

}

if (signer !== decode(entry).owner) {

throw new InvalidTransaction(

'Transfers can only be accepted by the new owner'

)

}

return state.set({

[address]: Buffer(0),

[getAssetAddress(asset)]: encode({name: asset, owner: signer})

})

})

}
```

The acceptTransfer function allows a user to accept a transfer of an asset and change the asset ownership.

## Accepting or Rejecting Transfers (Part II)

```js
const rejectTransfer = (asset, signer, state) => {

const address = getTransferAddress(asset)

return state.get([address])

.then(entries => {

const entry = entries[address]

if (!entry || entry.length === 0) {

throw new InvalidTransaction('Asset is not being transfered')

}

if (signer !== decode(entry).owner) {

throw new InvalidTransaction(

'Transfers can only be rejected by the potential new owner')

}

return state.set({

[address]: Buffer(0)

})

})

}
```

The rejectTransfer function allows a user to reject a transfer of an asset, and the asset owner will remain with the original user.

Within the user interface, any pending transfers for the selected user will appear under Accept Tuna. These can be accepted (with an immediate change in ownership), or rejected with the corresponding buttons.

## Accepting or Rejecting Transfers (Part III)

When we click Transfer, the proposal is sent to the Hyperledger Sawtooth network. If we switch the Select Holder field to the owner identified by the key starting with 03, we will see that we can now Accept or Reject this ownership change.

NOTE: If someone other than the owner tries to transfer ownership, you will see an error returned to the client from the Hyperledger Sawtooth network.

## Shutting Down Docker

Note: When we are done with this tutorial, run the following command to shut down Docker:

`$ docker-compose -f sawtooth-default.yaml down`

## Application Flow

[](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/148eb99c4e9410d799444b72fb7c6785/asset-v1:LinuxFoundationX+LFS171x+3T2017+type@asset+block/sawtooth-application-txflowdiagram.png)

Hyperledger Sawtooth allows entities to securely update and read the distributed ledger without involving a central authority. Developers create application and transaction processor business logic (smart contract).

Through the client application, users (fisherman, regulator, restaurant) are able to modify the state by creating and applying transactions.

Through a REST API, the client application creates a batch containing a single transaction, and submits it to the validator.

The validator applies the transaction using the transaction processor, which makes a change to the state (e.g., creating a record of a tuna catch).