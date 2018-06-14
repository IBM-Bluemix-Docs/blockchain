---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About Starter Plan
{: #overview}

{{site.data.keyword.blockchainfull}} Platform Starter Plan is an entry level option that enables organizations to simulate multi-organization blockchain networks, quickly develop applications, and work with sample smart contracts and business networks. It also boasts the same UI experience as other membership options, helping to eliminate any learning curve. Starter Plan networks are built on Hyperledger Fabric V1.1.
{:shortdesc}

**Notes**:
1. {{site.data.keyword.blockchainfull_notm}} Platform Starter Plan is a development and testing environment, and is not suitable for production workloads. If you need a production environment, see [About Enterprise Plan](enterprise_plan.html). You might check [Starter Plan considerations](#considerations) before you use Starter Plan.
2. Starter Plan moves from Beta to GA on June 14, 2018. If you have Beta networks, you might read the [migration considerations](#beta-to-ga).

Sign up for your [{{site.data.keyword.blockchainfull_notm}} membership ![External link icon](images/external_link.svg "External link icon")](https://console.bluemix.net/catalog/services/blockchain?env_id=ibm:yp:us-south&taxonomyNavigation=apps) and try the Starter Plan with [trial credits](howto/pricing.html#starter-plan-pricing) now! <!--Note that you must choose **US South** as the region in {{site.data.keyword.cloud_notm}} to create blockchain networks with Starter Plan.-->

## What Stater Plan offers

- **_One-click-ready network_**  
    Starter Plan provisions you a live blockchain network with a single click. Each network comes with an ordering service, CA's, two organizations (with one peer per organization), and a default channel on which to transact and deploy chaincode. {{site.data.keyword.blockchainfull_notm}} Platform handles the creation and configuration of this network (you'll be able to update it after it goes live), letting you focus on development. Starter Plan networks are built on Hyperledger Fabric V1.1, and use CouchDB as the ledger database. <!--The free trial provides you up to two organizations and two peers.-->
- **_Cost efficiency_**  
    The Starter Plan membership option provides many of the same blockchain capabilities as Enterprise Plan membership options, but at a lower cost. During a trial period of Starter Plan, you can provision a blockchain network with basic network resources for free.
- **_Multi-organization network simulation_**  
    You can use Starter Plan to simulate building a network with multiple organizations. You do not need to actually invite other organizations to your network, but can act as other organizations yourself. This mechanism enables you to learn how a new organization can join the network, how multiple organizations work together in the network, and so on. You can switch between your organizations from the Network Monitor to view and manage the network from different organizations' view.
    **Note**: It might cause extra cost if you add more resources than the free trial basic resources of two organizations and two peers.
<!-- - **_Easy to deploy sample applications_**  
    Starter Plan uses the Toolchain service in {{site.data.keyword.cloud_notm}} to deploy samples with simple clicks. After you deploy and launch a sample, the chaincode and applications automatically run for your blockchain network. For more information about sample applications, see [Deploying sample applications](howto/prebuilt_samples.html). -->
- **_{{site.data.keyword.blockchainfull_notm}} Platform: Develop application Integration_**  
    Starter Plan enables you to deploy business networks that you have developed on [{{site.data.keyword.blockchainfull_notm}} Platform: Develop](https://blockchaindevelop.mybluemix.net/login). For more information, see [Importing IBP: Develop applications](link).

## Target audiences

If you fit into one of the following situations, the Starter Plan is suitable for you to start your blockchain journey.
- **_Learning {{site.data.keyword.blockchainfull_notm}} Platform._**  
    If you are curious about {{site.data.keyword.blockchainfull_notm}} Platform or even new to blockchain, Starter Plan offers you a great way to learn how to develop and govern a real blockchain network. You can find the components that a network consists of, manage membership, learn how to deploy and manage chaincode (also known as "smart contracts"), how to add channels (and to manage channel permissions), and track when a new block is generated, just as in a production network.
- **_Building demo solutions on a live network._**  
    Starter Plan provides a powerful environment for demonstrating blockchain applications. The ready-to-use blockchain network enables quick presentations to colleagues, management, and partners through the operational and management tools that the Network Monitor provides.
- **_Moving beyond single organization development._**  
    Starter Plan enables you to act as multiple organizations, which allows you to see how the IBM Blockchain Platform manages collaborative tasks like channel creation and chaincode instantiation, as well as testing applications and invoking transactions. You can also invite others to collaborate in a Starter Plan network (as in Enterprise plans). This helps you you to build in a more realistic environment, with multiple parties endorsing chaincode and transactions.
- **_Iteratively develop and test blockchain applications._**  
    Starter Plan offers you a staging area to continuously develop and test your code on a blockchain network. Moving to cloud allows developers and testers to focus on functionalities and to easily move from unit test to functional test. Starter Plan provides the same blockchain network functionalities as well as operational and management tooling as the Enterprise Plan. After you are ready to push your project to one of the Enterprise plans, you can operate the same way as in Starter Plan, but with more opportunities to grow your network.


## Starter Plan considerations
{: #considerations}

Starter Plan is an entry point to {{site.data.keyword.blockchainfull_notm}} Platform and is for developing and testing purpose.  Check the following items before you use Starter Plan.

- **{{site.data.keyword.cloud_notm}} account requirement**  	
    You must have a paid {{site.data.keyword.cloud_notm}} account, for example, a **Pay-As-You-Go** type. All membership plans that {{site.data.keyword.blockchainfull_notm}} Platform offers require an  {{site.data.keyword.cloud_notm}} paid account. To upgrade your account to a Pay-As-You-Go type, go to **Manage** > **Billing and Usage** > **Billing** in the {{site.data.keyword.cloud_notm}} console, and click **Add Credit Card**.  
- **Differences from Enterprise Plan**
    - [CA](glossary.html#ca) and [ordering service](glossary.html#orderer) are not fault tolerant because each organization has only one CA and a network has only one [orderer](glossary.html#orderer).
    - Ordering service uses only [SOLO](glossary.html#SOLO) [consensus](glossary.html#consensus). A Starter Plan network consists of only one [orderer](glossary.html#orderer) that performs consensus for all peers.
    - [Hardware Security Module (HSM)](glossary.html#hsm) is not available to safeguard and manage digital keys for strong authentication and crypto processing.
- **Network resource limitation**  
    Starter Plan assigns 1 CPU and 2 Gi RAM for each peer, and 20 Gi storage for each {{site.data.keyword.cloud_notm}} service instance. 
- **Inactive network deletion**  
    After you create a Starter Plan network, if you don't visit the network or issue any transaction on it for 15 days, {{site.data.keyword.blockchainfull_notm}} Platform will delete the network.
    - If you don't need the network any more, you don't need to take any action and your network will be deleted automatically.
    - If you still need to use the network, you can keep it active by issuing transactions on it. You can find your Starter Plan  network in your [{{site.data.keyword.cloud_notm}} Dashboard ![External link icon](images/external_link.svg "External link icon")](https://console.bluemix.net/dashboard/apps/){:new_window}. If you don't have regular trasanctions to issue, follow the [instructions](howto/prebuilt_samples.html#deploying-sample-applications-in-starter-plan) to try the sample applications.
- **Maintenance and upgrade**
    Starter Plan maintenance and network updates are performed on a fixed schedule. During the maintenance period, you cannot provision new networks and might notice brief periods of network interruption.
- **Data retention**
    Starter Plan does not guarantee data retention with release upgrades, including moving from Beta to GA.
- **Migration considerations**
    - Migrating the data from a Starter Plan network to other membership plans is not currently supported. However, it is possible to migrate `.bna` files, chaincode, and applications that were tested on Starter Plan. For more information, see [Migrating from Starter Plan to Enterprise Plan](get_start_starter_plan.html#migrate).

<!--    - Starter Plan is built on Hyperledger Fabric V1.1.  If your chaincode is at Fabric V1.0 level, you need to upgrade your chaincode before you use it in Starter Plan. For more information, see [Updating chaincode for Hyperledger Fabric 1.1](knownissues.html/update-chaincode-fabric11).
-->

## Migrating from Beta to GA
{: #beta-to-ga}

Starter Plan moves to the GA stage on June 14, 2018. Upon GA, IBM Blockchain Platform offers $500 trial credits for each IBM Cloud account to create blockchain networks with Starter Plan. For more information about the trial credits, see [Consuming Starter Plan trial credits](howto/consum_sp_credit.html). Ensure that you have a paid IBM Cloud account, for example, a **Pay-As-You-Go** type.

Any blockchain networks that are created with Starter Plan Beta remains **free** until they are deleted **30 days** after the Starter Plan GA. Data migration is not supported from Starter Plan Beta networks to GA networks. **Your data in Beta networks will be lost.**  However, you can migrate your chaincode, business networks, and applications manually.
- If you have running chaincode in Beta networks, install and instantiate the chaincode in GA networks. For more information, see [Installing, instantiating, and updating a chaincode](howto/install_instantiate_chaincode.html).
- If you deployed a business network on Beta networks, deploy the business network with the `.bna` file on GA networks. For more information, see [Deploying a business network on Starter Plan](develop_starter.html).
- If you ran self-developed applications against Beta networks, update the API endpoints in your applications to point to GA network nodes. For more information, see [Adding network API endpoints to your application](v10_application.html#adding-network-api-endpoints-to-your-application).
