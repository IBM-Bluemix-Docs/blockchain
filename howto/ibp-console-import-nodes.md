---

copyright:
  years: 2019
lastupdated: "2019-07-10"

keywords: import nodes, another console, import a CA, import a peer, import admin identities, import an ordering service node

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}

# Importing nodes
{: #ibp-console-import-nodes}

The console includes the option to import nodes that are created by using another {{site.data.keyword.blockchainfull}} Platform console.
{:shortdesc}  

**Target audience:** This topic is designed for network operators who are responsible for creating, monitoring, and managing the blockchain network.

## Why import a node?
{: #ibp-console-import-nodes-why}

Import CAs, ordering services, and peers from other {{site.data.keyword.blockchainfull_notm}} Platform consoles when you need to operate them alongside nodes that already exist in your console. For example, you can use the import peer option when you want to join peers from organizations outside your console to channels in your console. As {{site.data.keyword.blockchainfull_notm}} Platform services are deployed across multiple  environments, it is likely that some service instances include only CAs and peers, whereas others host ordering services. Importing the disparate nodes into the console provides a way to view and operate these distributed components from a single user interface so they can transact together on the blockchain.

After you import nodes in the console, a robust set of operational capability becomes available, for example:
- Add new organizations to the consortium
- Create new channels
- Join peers to channels
- Install smart contracts on peers regardless of where they were deployed
- Instantiate smart contracts on channels
- Upgrade smart contracts on channels

When importing a node, you are required to provide its connection information. When you import a component, you do not actually import the physical component itself; instead, it uses the connection information to build a representation of the component in the console so that it can be operated from the console. Likewise, when you delete an imported node from the console, the node itself, which is still running at the location where it was deployed, is not deleted. Rather, it is only removed from the console where it was imported.  

After you import a node into the console, you can also modify its connection information by using the node's **Settings** tab.

Before you can import nodes into the console, they have to be exported from the {{site.data.keyword.blockchainfull_notm}} Platform console where they were created. The network operator can simply export the node information from the console to a `JSON` file.
{: note}

## Limitations
{: #ibp-console-import-limitations}

- You cannot import nodes from Starter plan or Enterprise plan networks.
- All nodes to be imported must have been deployed by using the {{site.data.keyword.blockchainfull_notm}} Platform console.
- You cannot patch nodes that you imported into the console.
- You cannot delete nodes that you imported into the console from the cluster where they were deployed. You can only remove the node from the console.
- If you are importing a node that is deployed on {{site.data.keyword.cloud_notm}} Private, you must ensure that the gRPC web proxy port used by the component is externally exposed to the console. For more information, see [Importing nodes from {{site.data.keyword.cloud_notm}} Private](#ibp-console-import-icp)
- When you open the tile of an imported node, the Fabric version is not visible and the **Usage and info** tab is not available.

## Start here: Gathering certificates or credentials
{: #ibp-console-import-start-here}

Before you can import an existing blockchain component from another {{site.data.keyword.blockchainfull_notm}} Platform service instance, you need to import the component's admin identity into your console wallet. Importing the identity into your console wallet streamlines node operation.  The network operator where the node was deployed should export the node admin identity from the wallet to a JSON file that you can [import](#ibp-console-import-nodes-admin-identities).  Typically, the node admin identity is the peer or orderer organization admin that was specified when the organization MSP definition was created. It should already be in the wallet of the console where the node resides.

### Importing admin identities into the console wallet
{: #ibp-console-import-nodes-admin-identities}

Each {{site.data.keyword.blockchainfull_notm}} Platform component is deployed with its own signing certificate, the signing cert, of a component administrator inside. When actions are performed against the component by the administrator, this signing certificate is attached to the transaction and validated against the component configuration. The keys allow the administrator to operate their components, such as by registering new users, creating a new channel or installing smart contracts on peers. If you want to use the console to operate an ordering service or peer that was created by using another console, you need to upload the associated admin identity to the console wallet. Then, you can associate the imported node with the identity the console wallet. These identities must be exported from the console where they were created and are required when the node is imported.

To import a new identity, open the **Wallet** tab and click **Add identity**. Click **Upload JSON** to browse to the JSON identity file that was exported by the network operator from where the node was created.

After you complete the **Add identity** panel and click submit, you can view the new admin identity in the wallet overview screen. Now you can refer to these identities when you import CA, peer, or ordering service components.

## Importing a CA
{: #ibp-console-import-ca}

A CA node is the blockchain component that issues certificates to all network entities (peers, ordering services, clients, and so on) so that these entities can communicate, authenticate, and ultimately transact. Each organization has their own CA that acts as their root of trust. You should add your organizations whether you are joining or building a blockchain consortium. You can learn more about CA's in the [overview of blockchain components](/docs/services/blockchain?topic=blockchain-blockchain-component-overview#blockchain-component-overview-ca).  

There are several reasons why you might want to import a CA into your console. After you import the CA, you can use it to register more peer users to the peer organization by clicking **Register user**. Or, you can use the CA to create additional admin identities for a peer or ordering service.

To import a CA to the {{site.data.keyword.blockchainfull_notm}} Platform console and operate it, the network operator must have already exported the CA from the {{site.data.keyword.blockchainfull_notm}} Platform where it was deployed. Importing a CA allows you to register new users and [enroll identities](/docs/services/blockchain/howto?topic=blockchain-ibp-console-identities#ibp-console-identities-enroll).

### Before you begin
{: #ibp-console-import-ca-before-you-begin}

- Ensure that you have already imported the CA's admin identity JSON file into your console wallet, or you have the administrator enroll id and secret for both the CA and the TLS CA that were specified when the CA was originally deployed.
- Ensure that the CA JSON file that was exported from the console where it was created is available.

### How to import a CA  
{: #ibp-console-import-nodes-howto-ca}

Importing a CA is performed from the **Nodes** tab.
1. Click **Add Certificate Authority**, followed by **Import an existing Certificate Authority**, and click **Next**.
2. Select the location where the CA was originally deployed from the **Certificate Authority location** drop-down list.
3. Click **Add file** to upload the CA JSON file that was exported from the console where it was originally deployed.
4. On the next panel, you can enter the enroll ID and secret that was used when the CA was deployed.
5. Lastly, enter the enroll ID and secret for the TLS CA that was used when the CA was deployed. When you deploy a CA, both a CA and a TLS CA are deployed together. The network operator can use the same enroll ID and secret for both, or they can specify unique enroll ID and secrets for the CA and the TLS CA when a CA is deployed.

After you have imported the CA into the console, you can use your CA to create new identities and generate the necessary certificates to operate your components and submit transactions to the network. To learn more, see [Managing certificate authorities](/docs/services/blockchain/howto?topic=blockchain-ibp-console-identities#ibp-console-identities-manage-ca).

## Importing an ordering service
{: #ibp-console-import-orderer}

An ordering service is the blockchain component that collects transactions from network members, orders the transactions, and bundles them into blocks. It is the common binding of blockchain consortiums and needs to be deployed if you are founding a consortium that other organizations will join. You can learn more about ordering services in the [overview of blockchain components](/docs/services/blockchain?topic=blockchain-blockchain-component-overview#blockchain-component-overview-orderer).

Importing an ordering service into the console allows you to create new channels for peers to transact privately.

### Before you begin
{: #ibp-console-import-orderer-before-you-begin}

Before you can import an ordering service, you need to gather the following information:

- Ensure that you have already [imported the ordering service's admin identity JSON file](#ibp-console-import-nodes-admin-identities) into your console wallet.
- Ensure that the ordering service JSON file that was exported from the console where it was created is available.

### How to import an ordering service
Importing an ordering service is performed from the **Nodes** tab.
1. Click the **Add ordering service**, followed by **Import an existing ordering service** and click **Next**.
2. Select the location where the ordering service was originally deployed from the **Certificate Authority location** drop-down list.
3. Click **Add file** to upload the ordering service JSON file that was exported from the console where it was originally deployed. Note that if this was a five node Raft ordering service, you should have a single file with the connection information for all five ordering nodes in the file.
4. Set the admin identity for the ordering service by clicking **Existing identity** and selecting the ordering service admin identity that you imported into your console wallet.

After you have imported the ordering service into the console, you can add new organization members and select the ordering service when creating new channels.

## Importing a peer
{: #ibp-console-import-peer}

A peer node is the blockchain component that maintains a ledger and runs a smart contract to perform query and update operations on the ledger. Organization members own and maintain peers.  Each organization that joins a consortium should deploy at least one peer and minimally two for High Availability (HA). You can learn more about peers in the [overview of blockchain components](/docs/services/blockchain?topic=blockchain-blockchain-component-overview#blockchain-component-overview-peer).

After you import a peer into the console, you can install smart contracts on the peer and join the peer to other channels in your blockchain.

**Note:** If you need to add more peers to the peer organization or create additional admin identities for a peer, you need to import the peer's CA and then use that CA to perform those operations.

### Before you begin
{: #ibp-console-import-peer-before-you-begin}

Before you can import a peer, you need to gather the following information:

- Ensure that you have already [imported the peer's admin identity JSON file](#ibp-console-import-nodes-admin-identities) into your console wallet.
- Ensure that the peer JSON file that was exported from the console where it was created is available.

### How to import a peer
{: #ibp-console-import-peer-howto}

Importing a peer is performed from the **Nodes** tab.
1. Click **Add Peer**, followed by **Import an existing peer** and then click **Next**.
2. Select the location where the peer was originally deployed from the **Certificate Authority location** drop-down list.
3. Click **Add file** to upload the peer JSON file that was exported from the console where it was originally deployed.
4. Set the admin identity for the peer by clicking **Existing identity** and selecting the peer admin identity that you imported into your console wallet.  

After you import the peer into the console, you can install smart contracts on the peer and join the peer to channels in your blockchain.

## Importing an organization MSP definition
{: #ibp-console-import-msp}

You need to import an organization's MSP definition if the MSP was deployed by using another {{site.data.keyword.blockchainfull_notm}} Platform service instance console and you plan to create or update a channel that uses that MSP defintion. Also, if you plan to create a peer or ordering service that is part of an organization MSP that was deployed in another console, you need to import the MSP and the associated MSP admin identity.  The network operator who created the MSP needs to export the organization MSP definition and the corresponding admin identity to JSON files and share them with you.

- If you plan to create a peer or ordering service that is part of the organization, import the associated MSP admin identity into your wallet.
- Importing the organization MSP definition is performed from the **Organizations** tab.
- Click **Import MSP definition** to upload the JSON file
- (Optional) If you imported the MSP admin identity into your wallet, check the checkbox `I have an administrator identity for the MSP definition`. If you do not select this option, when you subsequently try to create a peer or ordering service, this organization MSP definition will not be listed in the MSP drop-down list.

## Importing nodes from {{site.data.keyword.cloud_notm}} Private
{: #ibp-console-import-icp}

You can import nodes that were created on {{site.data.keyword.cloud_notm}} Private into consoles that have been deployed on other {{site.data.keyword.cloud_notm}} Private clusters or on {{site.data.keyword.cloud_notm}}. However, you need to ensure that the port used by the gRPC URL of your nodes are exposed from outside the cluster. If you are deploying {{site.data.keyword.cloud_notm}} Private behind a firewall, you need to enable a passthru, by using white listing for example, to allow the console outside the cluster to communicate with your nodes.

As an example, you can find the JSON file of a peer that was exported from {{site.data.keyword.cloud_notm}} Private below. To communicate with the peer from another console, you need to ensure that the `grpcwp_url` port, port 32403 in this example, is open to external traffic.

```
{
    "name": "peer",
    "grpcwp_url": "https://9.30.252.107:32403", \\ensure that port 32403 is externally exposed
    "api_url": "grpcs://9.30.252.107:30891",
    "operations_url": "https://9.30.252.107:30222",
    "type": "fabric-peer",
    "msp_id": "org1msp",
    "pem": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUNGekNDQWI2Z0F3SUJBZ0lVUi9zMGxGTG5ZNmdWRmV1Mlg5ajkrY3JDZFBrd0NnWUlLb1pJemowRUF3SXcKWFRFTE1Ba0dBMVVFQmhNQ1ZWTXhGekFWQmdOVkJBZ1REazV2Y25Sb0lFTmhjbTlzYVc1aE1SUXdFZ1lEVlFRSwpFd3RJZVhCbGNteGxaR2RsY2pFUE1BMEdBMVVFQ3hNR1JtRmljbWxqTVE0d0RBWURWUVFERXdWMGJITmpZVEFlCkZ3MHhPVEEyTVRBeE9USXhNREJhRncwek5EQTJNRFl4T1RJeE1EQmFNRjB4Q3pBSkJnTlZCQVlUQWxWVE1SY3cKRlFZRFZRUUlFdzVPYjNKMGFDQkRZWEp2YkdsdVlURVVNQklHQTFVRUNoTUxTSGx3WlhKc1pXUm5aWEl4RHpBTgpCZ05WQkFzVEJrWmhZbkpwWXpFT01Bd0dBMVVFQXhNRmRHeHpZMkV3V1RBVEJnY3Foa2pPUFFJQkJnZ3Foa2pPClBRTUJCd05DQUFUYUtyN2srUHNYeXFkWkdXUHlJUXlGMGQxUkFFdmdCYlpkVnlsc3hReWZOcUdZS0FZV3A0SFUKVUVaVHVVNmtiRXN5Qi9aOVJQWEY0WVNGbW8reTVmSkhvMXd3V2pBT0JnTlZIUThCQWY4RUJBTUNBUVl3RWdZRApWUjBUQVFIL0JBZ3dCZ0VCL3dJQkFUQWRCZ05WSFE0RUZnUVUrcnBNb2dRc3dDTnZMQzJKNmp2cElQOExwaE13CkZRWURWUjBSQkE0d0RJY0VDUjc4YTRjRXJCRE5DakFLQmdncWhrak9QUVFEQWdOSEFEQkVBaUJGWmpMWU9XZUMKLy92L2RNMHdYNUxZT3NCaHFFNnNQZ1BSWWppOTZqT093QUlnZEppZDU0WmxjR2h0R3dEY3ZoZE02RVlBVFpQNwpmS29IMDZ3ZFhpK3VzVXM9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K"
}
```
