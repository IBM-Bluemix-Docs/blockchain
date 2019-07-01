---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: update data, private data, smart contract, CouchDB indexes, cross chaincode transaction

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}

# Ecriture de contrats intelligents
{: #develop-smart-contracts}

Le code blockchain, également désigné sous l'appellation de contrats intelligents, est un logiciel qui vous permet de lire et de mettre à jour des données dans le registre de blockchain. Le code blockchain peut transformer la logique applicative en programme exécutable accepté et vérifié par tous les membres du réseau de blockchain. La logique applicative inclut la définition de ressources échangées entre les parties. Elle comporte également les dispositions nécessaires à l'exécution d'une transaction. La conversion de ces règles en code dans une blockchain permet aux entreprises de rationaliser les processus et les audits métier et de réduire les énormes volumes de traitement manuel et de paperasses.

Supposons, par exemple, qu'un réseau de concessionnaires automobiles, de compagnies d'assurances et d'organismes de réglementation gouvernementaux, décident d'utiliser la technologie blockchain pour suivre la propriété des véhicules. Le code blockchain peut nécessiter que tous les véhicules possèdent un numéro d'immatriculation et d'identification du véhicule valides pour pouvoir être ajoutés au réseau. Lors de la vente d'un véhicule, le code blockchain peut nécessiter que les fonds soient placés sur un compte bloqué, jusqu'à ce que le véhicule soit enregistré auprès de son nouveau propriétaire par un régulateur. Une fois le nouveau enregistrement effectué, le nouveau propriétaire sera enregistré et les fonds transférés automatiquement.

Le tutoriel ci-après vous permet d'aborder les concepts de base relatifs à la génération de code blockchain :

- [Comment commencer à écrire du code blockchain](/docs/services/blockchain/howto?topic=blockchain-develop-smart-contracts#develop-smart-contracts-write)
- [Relations entre le code blockchain et les données](/docs/services/blockchain/howto?topic=blockchain-develop-smart-contracts#develop-smart-contracts-data)
- [Transactions entre codes blockchain](/docs/services/blockchain/howto?topic=blockchain-develop-smart-contracts#develop-smart-contracts-cross-chaincode)

Le tutoriel présente également des aspects importants de Fabric qui sont accessibles via le code blockchain :

- [Utilisation des index avec couchDB](/docs/services/blockchain/howto?topic=blockchain-develop-smart-contracts#develop-smart-contracts-indexes)

## Ecriture de code blockchain
{: #develop-smart-contracts-write}

Le code blockchain peut être écrit dans différents langages et le {{site.data.keyword.blockchainfull_notm}} Platform prend en charge le code blockchain écrit en Go et Node.js. Il permet aux utilisateurs d'interroger et de modifier des données qui sont stockées dans le code blockchain à l'aide d'API fournies par l'interface de blockchain Fabric. Les données de la blockchain sont stockées dans des paires clé/valeur dans le World State du [registre](https://hyperledger-fabric.readthedocs.io/en/release-1.2/ledger/ledger.html){: external} de canal. Le code blockchain utilise des commandes get pour extraire des valeurs et des commandes put pour créer ou mettre à jour des valeurs. Grâce à ces opérations de base, vous pouvez générer des fonctions qui définissent les règles métier de votre réseau. Ces fonctions peuvent être appelées par vos applications et présentées aux utilisateurs finaux du réseau. Pour continuer à utiliser l'exemple de réseau de véhicules, vous pouvez créer une fonction qui autorise un concessionnaire automobile à utiliser une commande `PUT` pour ajouter une nouvelle voiture au registre si un numéro d'identification du véhicule valide est fourni.

Pour apprendre à commencer à écrire du code blockchain, consultez le [tutoriel Chaincode for developers](https://hyperledger-fabric.readthedocs.io/en/release-1.2/chaincode4ade.html){: external} dans la documentation Hyperledger Fabric. Ce tutoriel vous guide tout au long des étapes de construction d'un exemple de code blockchain qui crée et lit des ressources et vous présente les API qui sont utilisées au cours du processus. Vous pouvez également trouver le guide de référence des API de code blockchain pour tous les langages de code blockchain. Des exemples supplémentaires sont fournis dans le dossier chaincode du [référentiel Fabric samples](https://github.com/hyperledger/fabric-samples){: external}.  

Un contrat intelligent est généralement en mesure de valider des demandes, d'appliquer les règles métier et de retourner un résultat déterministe. Cependant, il peut arriver que des faits supplémentaires soient nécessaires ou que le réseau métier souhaite s'assurer que les informations fournies par les clients sont des faits réels. Hyperledger Fabric n'empêche pas les appels externes à des systèmes tiers depuis les contrats intelligents. Il est toutefois de la responsabilité du développeur du contrat intelligent de garantir que les ensembles de lecture/écriture résultants sont déterministes.
{:note}

## Installation du code blockchain
{: #develop-smart-contracts-install}

Etant donné que le code blockchain fournit la structure des transactions sur un canal, il doit être installé sur tous les homologues joints sur le canal qui souhaitent utiliser le code blockchain pour mettre à jour ou interroger le registre de canal. Ensuite, un membre du canal peut instancier le code blockchain sur un canal et définir la règle d'adhésion du code blockchain. L'installation et l'instanciation du code blockchain peuvent être effectuées à l'aide de l'interface utilisateur d'{{site.data.keyword.blockchainfull_notm}} Platform, de l'interface de ligne de commande Fabric Peer ou à partir d'une application client utilisant des logiciels SDK Fabric. Si vous utilisez {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}, consultez le [tutoriel Déployer un contrat intelligent sur le réseau](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts) pour apprendre à déployer un code blockchain à l'aide de la console {{site.data.keyword.blockchainfull_notm}} Platform. Si vous utilisez un plan Starter ou un plan Enterprise, voir [Installation, instanciation et mise à jour d'un code blockchain](/docs/services/blockchain/howto?topic=blockchain-install-instantiate-chaincode#install-instantiate-chaincode) pour apprendre à déployer un code blockchain à l'aide de l'interface utilisateur du Moniteur réseau.

## Code blockchain et données
{: #develop-smart-contracts-data}

Chaque canal ne peut avoir qu'un seul registre, et les données de ce registre sont partitionnées par une clé unique et le code blockchain qui a ajouté la paire clé-valeur au registre. Les membres peuvent uniquement lire ou mettre à jour les données du registre de canal à l'aide de la clé appropriée et du code blockchain associé. Les données auxquelles un code blockchain peut accéder sont appelées espace de nom du code blockchain et l'ensemble des données du registre figurent dans l'espace de nom d'un code blockchain. Un code blockchain peut interagir avec des données en dehors de son espace de nom uniquement à l'aide d'une [transaction entre codes blockchain](/docs/services/blockchain/howto?topic=blockchain-develop-smart-contracts#develop-smart-contracts-cross-chaincode) pour que le code blockchain puisse accéder aux données pertinentes.

Nous pouvons utiliser le code blockchain fabcar du référentiel d'exemples Fabric comme exemple de l'interaction du code blockchain avec les données. L'espace de nom est créé lorsque le contrat intelligent est instancié. Certains codes blockchain acceptent un ensemble d'arguments de paire clé-valeur lorsque le code blockchain est instancié et ils utilisent ces données pour initialiser l'espace de nom. Le code blockchain fabcar du référentiel d'exemples Fabric n'accepte aucun argument lorsqu'il est instancié. Pour fabcar, vous devez ajouter des données à l'espace de noms à l'aide de la fonction initLedger ou createCar. Par exemple, la transmission de l'argument `{"Args":["createCar",'CAR1', 'Honda', 'Accord', 'Black', 'Tom']}` fait de la paire clé-valeur `{Key='CAR1', value={'Honda', 'Accord', 'Black', 'Tom'}}` l'espace de nom fabcar.

Seul le code blockchain fabcar peut modifier ces données. Supposons que l'utilisateur souhaite transférer la voiture à un nouveau propriétaire à l'aide de la fonction changeCarOwner ci-dessous :
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

Vous pouvez appeler le code blockchain à l'aide des arguments suivants :
```
{"Args":["changeCarOwner",'CAR1','Mark']}
```
{:codeblock}

le code blockchain utilise ensuite les commandes get pour générer un ensemble de lectures à partir de l'espace de nom du code blockchain. Il utilise les commandes put pour créer l'ensemble d'écritures de transaction. L'appel de code blockchain crée également un ID transaction unique.
```
TxId = Txid1
Read Set: `{Key='CAR1', value[3]='Tom'}`
Write Set: `{Key='CAR1', value[3]='Mark'}`
```
{:codeblock}

Chaque homologue de validation sur lequel est installé le code blockchain va simuler les transactions à l'aide du jeu de lectures et du jeu d'écritures. Si les simulations de chaque homologue sont cohérentes, elles sont considérées comme étant valides et elles peuvent être validées dans le registre. Après la transaction, l'espace de nom fabcar devient `{Key='CAR1', value='Honda', 'Accord', 'Black', 'Mark'}`. Notez que le propriétaire est passé de Tom à Mark.

La relation 1-1 entre le code blockchain et les données crée d'importantes considérations pour le développement de réseaux et d'applications. Le logiciel de code blockchain ne doit être mis à jour que par l'installation d'un code blockchain de même nom et de version différente, et non par l'utilisation d'un nouveau code blockchain. Cette procédure de mise à jour préserve l'espace de nom du code blockchain et vous permet de continuer à utiliser les données existantes. Vous pouvez aussi utiliser un code blockchain différent pour retreindre l'accès aux données sensibles, ou lire et écrire des données en parallèle.

## Transactions entre codes blockchain
{: #develop-smart-contracts-cross-chaincode}

Vous pouvez utiliser un code blockchain pour appeler d'autres codes blockchain. Un code blockchain peut ainsi interroger et écrire des données à l'extérieur de son espace de nom. Un code blockchain peut à la fois lire et mettre à jour des données à l'aide d'un code blockchain instancié sur le même canal. Il peut cependant uniquement interroger des données à l'aide d'un code blockchain sur différents canaux. L'organisation qui appelle le code blockchain d'origine doit être autorisé à appeler le code blockchain qui est la cible de la transaction.

Par exemple, vous pouvez utiliser la fonction `crossChaincodeChangeCarOwner` ci-dessous pour appeler fabcar depuis un autre code blockchain. Etant donné que a fonction met à jour les données en changeant le propriétaire de la voiture, elle doit appeler un code blockchain fabcar instancié sur le même canal.
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

Si vous créez un nouveau contrat à l'aide de ce code et appelez la fonction `crossChaincodeChangeCarOwner`, la transaction générera un ID transaction et un ensemble d'écritures.
```
Contract: newContract
TxId = Txid2
Write Set: `{Key='CAR1', value[3]='Mark'}`
```
{:codeblock}

Ce TXid et cet ensemble d'écritures sera transmis au code blockchain fabcar.
```
Contract: fabcar
TxId = Txid2
Read Set: `{Key='CAR1', value[3]='Mark'}`
Write Set: `{Key='CAR1', value[3]='Joe'}`
```
{:codeblock}

Etant donné que `fabcar` est sur le même canal que `newContract`, la fonction `crossChaincodeChangeCarOwner` est autorisée à écrire dans l'espace de nom `fabcar`. Le nouvel espace de nom `fabcar` sera `{Key='CAR1', value='Honda', 'Accord', 'Black', 'Joe'}`.


## Utilisation des index avec CouchDB
{: #develop-smart-contracts-indexes}

Si vous utilisez CouchDB comme base de données d'état, vous pouvez exécuter des requêtes de données JSON depuis votre code blockchain sur les données d'état du canal. Nous vous recommandons fortement de créer des index pour vos requêtes JSON et de les utiliser dans votre code blockchain. Les index permettent à vos applications d'extraire les données de manière aussi efficace que votre réseau ajoute des blocs de transaction et des entrées supplémentaires dans le World State.

Pour plus d'informations sur CouchDB et la façon de définir des index, voir [CouchDB as the State Database](https://hyperledger-fabric.readthedocs.io/en/release-1.2/couchdb_as_state_database.html){: external} dans la documentation Hyperledger Fabric. Vous trouverez également un exemple utilisant un index avec un code blockchain dans le [tutoriel Fabric CouchDB](https://hyperledger-fabric.readthedocs.io/en/release-1.2/couchdb_tutorial.html){: external}. Consultez la section relative aux [meilleures pratiques lors de l'utilisation de CouchDB](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-app-couchdb-indices) dans le tutoriel Développement d'applications pour plusd'informations sur l'interrogation de données depuis vos applications.
