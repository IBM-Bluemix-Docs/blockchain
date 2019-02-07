---

copyright:
  years: 2017, 2019
lastupdated: "2018-02-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Writing smart contracts
{: #develop-smart-contracts}

***[Is this page helpful? Tell us.](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***

Chaincode, also referred to as smart contracts, is software that allows you to read and update data on the blockchain ledger. Chaincode can turn business logic into an executable program agreed to and verified by all members of the blockchain network. Business logic includes the definition of assets traded between parties. It also consists of the terms and conditions required for a transaction to be executed. Turning these rules into code on a blockchain allow businesses to streamline business processing and auditing and reduce large amounts of manual processing and paperwork.

As an example, imagine that a network of car dealerships, insurance companies and government regulators decided to use blockchain to track vehicle ownership. The chaincode may require that all vehicles have a valid registration and vehicle identification number in order to be added to the network. When a vehicle is sold, the chaincode may require that funds are placed in escrow until the vehicle is registered to its new owner by a regulator. When the new registration is complete, the new owner will be recorded and the funds transferred automatically.

The following tutorial will take you through the basic aspects of building chaincode, including:

- [How to get started writing chaincode](/docs/services/blockchain/howto/develop_chaincode.html#develop-smart-contracts-write)
- [The relationship between chaincode and data](/docs/services/blockchain/howto/develop_chaincode.html#develop-smart-contracts-data)
- [Cross chaincode transactions](/docs/services/blockchain/howto/develop_chaincode.html#develop-smart-contracts-cross-chaincode)

The tutorial also introduces important aspects of fabric that are accessible through chaincode:

- [Using indexes with couchDB](/docs/services/blockchain/howto/develop_chaincode.html#develop-smart-contracts-indexes)

## Writing chaincode
{: #develop-smart-contracts-write}

Chaincode can be written in multiple languages, and the {{site.data.keyword.blockchainfull_notm}} Platform supports chaincode written in Go and Node.js. Chaincode allows users query and change data that is stored in the blockchain by using APIs that the Fabric Chaincode interface provides. Data on the blockchain is stored in key-value pairs in the world state of the channel [ledger ![External link icon](../images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/release-1.2/ledger/ledger.html "ledger"). Chaincode uses get commands to retrieve values and use put commands to create or update values. Using these basic operations, you can build functions that define the business rules of your network. These functions can be invoked by your applications and surfaced to end users of the network. To continue using the vehicle network example, you can create a function that allows a car dealership to use a put command to add a new car to the ledger only if they provide a valid vehicle ID number.

You can learn how to start writing chaincode by visiting the [Chaincode for developers tutorial ![External link icon](../images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/latest/chaincode4ade.html "chaincode for developers tutorial") in the Hyperledger Fabric community documentation. The tutorial will take you through the construction of a simple chaincode that creates and reads assets and introduces you to which APIs are used in the process. You can also find the chaincode API reference guide for all chaincode languages. There are additional examples in the chaincode folder of the [Fabric samples repository ![External link icon](../images/external_link.svg "External link icon")](https://github.com/hyperledger/fabric-samples "Fabric samples").

## Installing Chaincode
{: #develop-smart-contracts-install}

Because chaincode provides the structure of transactions on a channel, a chaincode needs to be installed on all the peers joined to the channel that want use the chaincode to update or query the channel ledger. Then one member of the channel can then instantiate the chaincode on a channel and set the chaincode's endorsement policy. Install and instantiation of chaincode can be performed using the Network Monitor UI, the Fabric Peer command line interface, or from a client application using the [Fabric SDK](/docs/services/blockchain/v10_application.html#dev-app-operate-sdk). To learn how to use the Network Monitor UI to deploy chaincode, see [Installing, instantiating, and updating a chaincode](/docs/services/blockchain/howto/install_instantiate_chaincode.html#install-instantiate-chaincode).

## Chaincode and data
{: #develop-smart-contracts-data}

Each channel only has one ledger, and the data on that ledger is partitioned by a unique key and the chaincode that added the key value pair to the ledger. Members can only read or update data on the channel ledger by using the correct key and the associated chaincode. The data that can be accessed by a chaincode is referred to as that chaincode's namespace and all data on the ledger is within the namespace of one chaincode. A chaincode can interact with data outside of its namespace only by using a [cross chaincode transaction](/docs/services/blockchain/howto/develop_chaincode.html#develop-smart-contracts-cross-chaincode) to the chaincode that can access the relevant data.

We can use the fabcar chaincode from the Fabric samples repository as an example of how chaincode interacts with data. The namespace is created when the smart contract is instantiated. Some chaincode accepts a set of key value pair arguments when the chaincode is instantiated and use that data to initialize the namespace. The fabcar chaincode from the Fabric samples repository does not accept any arguments when it is instantiated. For fabcar, you need to add data to the namespace using the initLedger or createCar function. For instance, passing the argument `{"Args":["createCar",'CAR1', 'Honda', 'Accord', 'Black', 'Tom']}` will make the key value pair of `{Key='CAR1', value={'Honda', 'Accord', 'Black', 'Tom'}}` the fabcar namespace.

Only the fabcar chaincode can change this data. Assume that the user wants to transfer the car to a new owner by using the changeCarOwner function below:
```
func (s *SmartContract) changeCarOwner(APIstub shim.ChaincodeStubInterface, args []string) sc.Response {

	if len(args) != 2 {
		return shim.Error("Incorrect number of arguments. Expecting 2")
	}

	carAsBytes, _ := APIstub.GetState(args[0])
	car := Car{}

	json.Unmarshal(carAsBytes, &car)
	car.Owner = args[1]

	carAsBytes, _ = json.Marshal(car)
	APIstub.PutState(args[0], carAsBytes)

	return shim.Success(nil)
}
```
{:codeblock}

You can invoke the chaincode by using the following arguments:
```
{"Args":["changeCarOwner",'CAR1','Mark']}
```
{:codeblock}

The chaincode then uses the get commands to generate a read set from the chaincode namespace. It uses the put commands to create the transaction write set. The chaincode invoke also creates a unique transaction ID.
```
TxId = Txid1
Read Set: `{Key='CAR1', value[3]='Tom'}`
Write Set: `{Key='CAR1', value[3]='Mark'}`
```
{:codeblock}

Each endorsing peer with the chaincode installed will simulate the transactions using the read set and the write set. If the simulations by each peer are consistent, the transactions is considered valid and can be committed to the ledger. After the transaction, the fabcar namespace will become `{Key='CAR1', value='Honda', 'Accord', 'Black', 'Mark'}`. Notice the owner has changed from Tom to Mark.

The 1-1 relationship between chaincode and data creates important considerations for developing networks and applications. Chaincode software should be updated by installing a chaincode with the same name and a different version, rather than the use of a new chaincode. This update procedure preserves the chaincode namespace and will allow you to continue to use the existing data. You can also use different chaincode to restrict access to sensitive data, or read and write data in parallel.

## Cross chaincode transactions
{: #develop-smart-contracts-cross-chaincode}

You can use a chaincode to invoke other chaincodes. This allows a chaincode to query and write to data outside of its namespace. Chaincode can both read and update data using chaincode instantiated on the same channel. However they can only query data using chaincode on different channels. The organization invoking the original chaincode needs to be authorized to invoke the chaincode that is the target of the transaction.

For example, you can use the `crossChaincodeChangeCarOwner` function below to call fabcar from another chaincode. Because the function updates data by changing the car owner, it needs to call a fabcar chaincode instantiated on the same channel.
```
func (s *SmartContract) crossChaincodeChangeCarOwner(APIstub shim.ChaincodeStubInterface, args []string) sc.Response {
	newOwnerArgs := toChaincodeArgs("changeCarOwner", args[0], args[1])

	chaincodeName := "fabcar"
	channelName := "defaultchannel"

	APIstub.InvokeChaincode(chaincodeName, newOwnerArgs, channelName)

	return shim.Success(nil)
}
```
{:codeblock}

If you create a new contract using this code and invoke the function `crossChaincodeChangeCarOwner`, the transaction will generate new a transaction ID and a write set.
```
Contract: newContract
TxId = Txid2
Write Set: `{Key='CAR1', value[3]='Mark'}`
```
{:codeblock}

This TXid and write set will pass to the fabcar chaincode.
```
Contract: fabcar
TxId = Txid2
Read Set: `{Key='CAR1', value[3]='Mark'}`
Write Set: `{Key='CAR1', value[3]='Joe'}`
```
{:codeblock}

Because `fabcar` is on the same channel as `newContract`, the `crossChaincodeChangeCarOwner` function is allowed to write to the `fabcar` namespace. The new `fabcar` namespace will be `{Key='CAR1', value='Honda', 'Accord', 'Black', 'Joe'}`.


## Using indexes with CouchDB
{: #develop-smart-contracts-indexes}

If you use CouchDB as your state database, you can perform JSON data queries from your chaincode against the channel's state data. It is strongly recommended that you create indexes for your JSON queries and use them in your chaincode. Indexes allow your applications to retrieve data efficiently as your network adds additional blocks of transactions and entries in the world state.

For more information about CouchDB and how to set up indexes, see [CouchDB as the State Database ![External link icon](../images/external_link.svg "External link icon")](http://hyperledger-fabric.readthedocs.io/en/release-1.1/couchdb_as_state_database.html "CouchDB as the State Database"){:new_window} in the Hyperledger Fabric documentation. You can also find an example that uses an index with chaincode in the [Fabric CouchDB tutorial ![External link icon](../images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/release-1.2/couchdb_tutorial.html). Visit [Best Practices when using CouchDB](/docs/services/blockchain/v10_application.html#dev-app-couchdb-indices) in the Developing applications tutorial for more information on how to query data from your applications.
