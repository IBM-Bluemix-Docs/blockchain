---

copyright:
  years: 2019
lastupdated: "2019-06-18"

keywords: smart contract, private data, private data collection, anchor peer

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

# Tutoriel Déployer un contrat intelligent sur le réseau
{: #ibp-console-smart-contracts}

Un contrat intelligent est le code, parfois appelé chaincode, qui vous permet de lire et de mettre à jour des données dans le registre de blockchain. Un contrat intelligent peut transformer la logique applicative en programme exécutable accepté et vérifié par tous les membres d'un réseau de blockchain. Ce tutoriel est la troisième partie de la [série d'exemples de tutoriel réseau](#ibp-console-smart-contracts-structure) ; il explique comment déployer des contrats intelligents pour lancer des transactions sur le réseau de blockchain.
{:shortdesc}

Si vous utilisez la version d'essai bêta d'{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}, il est probable que certains panneaux sur votre console ne correspondront pas à ceux de la documentation actuelle, qui est mise à jour avec l'instance de service disponible globalement. Pour bénéficier des toutes dernières fonctionnalités, nous vous encourageons à ce stade à mettre en service une nouvelle instance de service disponible globalement en suivant les instructions de la section [Initiation à {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}](/docs/services/blockchain/howto?topic=blockchain-ibp-v2-deploy-iks#ibp-v2-deploy-iks).
{: important}

**Public cible :** Cette rubrique s'adresse aux opérateurs réseau qui sont responsables de la création, de la surveillance et de la gestion du réseau de blockchain. Les développeurs d'applications peuvent également être intéressés par les sections qui font référence à la création d'un contrat intelligent.

## Série d'exemples de tutoriel réseau
{: #ibp-console-smart-contracts-structure}

Cette série de tutoriels en trois parties vous guide tout au long du processus de création et d'interconnexion d'un réseau Hyperledger Fabric à plusieurs noeuds relativement simple à l'aide de la console {{site.data.keyword.blockchainfull_notm}} Platform pour le déploiement d'un réseau dans votre cluster Kubernetes, ainsi que l'installation et l'instanciation d'un contrat intelligent.

* [Générer un réseau](/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network) : Ce tutoriel vous guide tout au long du processus d'hébergement d'un réseau par la création d'un service de tri et d'un homologue.
* [Rejoindre un réseau](/docs/services/blockchain/howto?topic=blockchain-ibp-console-join-network#ibp-console-join-network) : Ce tutoriel vous guide tout au long du processus permettant de rejoindre un réseau existant en créant un homologue et en le joignant à un canal.
* **Déployer un contrat intelligent sur le réseau** : Ce tutoriel fournit des informations sur l'écriture d'un contrat intelligent et son déploiement sur votre réseau.

Vous pouvez utiliser les étapes de ces tutoriels pour générer un réseau comportant plusieurs organisations dans un cluster à des fins de développement et de test. Utilisez le tutoriel **Générer un réseau** si vous voulez former un consortium de blockchain en créant un noeud de service de tri et en ajoutant des organisations. Utilisez le tutoriel **Rejoindre un réseau** pour connecter un homologue au réseau. L'utilisation des tutoriels par différents membres de consortium vous permet de créer un réseau de blockchain réellement **distribué**.  

Ce dernier tutoriel vous montre comment créer et packager un contrat intelligent, comment l'installer sur un homologue et comment l'instancier sur un canal.  

Les contrats intelligents sont installés sur des homologues et instanciés sur des canaux. **Tous les membres qui souhaitent soumettre des transactions ou lire des données à l'aide d'un contrat intelligent doivent installer ce contrat sur leur homologue.** Un contrat intelligent est défini par son nom et sa version. Par conséquent, le nom et la version du contrat installé doivent être cohérents sur tous les homologues sur le canal qui va exécuter le contrat intelligent.

Une fois qu'un contrat intelligent est installé sur les homologues, un seul membre réseau instancie le contrat sur le canal. Ce membre réseau doit avoir rejoint le canal pour pouvoir effectuer cette action. L'instanciation met à jour le registre à l'aide des données initiales utilisées par le contrat intelligent, puis elle démarre les conteneurs de contrat intelligent sur les homologues joints au canal avec le contrat intelligent installé. Les homologues peuvent ensuite utiliser les conteneurs en cours d'exécution pour effectuer des transactions.  
- **Un seul membre réseau doit instancier un contrat intelligent.**
- **Si un homologue avec un contrat intelligent installé rejoint un canal où la même version de contrat intelligent est déjà instanciée, le conteneur de contrat intelligent démarre automatiquement. **  

Dans ce tutoriel, nous allons passer en revue les étapes d'utilisation de la console {{site.data.keyword.blockchainfull_notm}} Platform pour gérer le déploiement de contrats intelligents sur votre réseau :

- [Installer des contrats intelligents sur vos homologues](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-install).
- [Instancier ces contrats sur des canaux ](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-instantiate).
- [Indiquer des règles d'adhésion](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-endorse).
- [Mettre à niveau les règles et le code de contrat intelligent](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-upgrade).


## Avant de commencer

Avant d'installer un contrat intelligent, vérifiez que vous remplissez bien les conditions suivantes.

- Vous devez [générer un réseau](/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network) ou [rejoindre un réseau](/docs/services/blockchain/howto?topic=blockchain-ibp-console-join-network#ibp-console-join-network) à l'aide de votre console {{site.data.keyword.blockchainfull_notm}} Platform.
- Comme les contrats intelligents sont installés sur des homologues, assurez-vous que vous [ajoutez des homologues](/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network-create-peer-org1) à votre console.  
- Les contrats intelligents sont instanciés sur un canal. Par conséquent, vous devez [créer un canal](/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network-create-channel) ou [rejoindre un canal](/docs/services/blockchain/howto?topic=blockchain-ibp-console-join-network#ibp-console-join-network-join-peer-org2) à l'aide de la console.

## Etape 1 : Ecrire un contrat intelligent

La console {{site.data.keyword.blockchainfull_notm}} gère le *déploiement* des contrats intelligents et non leur développement. Si vous souhaitez développer des contrats intelligents, vous pouvez vous initier à l'aide de tutoriels fournis par la communauté Hyperledger Fabric et des outils proposés par {{site.data.keyword.IBM_notm}}.

- Pour en savoir plus sur la façon dont les contrats intelligents peuvent être utilisés pour mener des transactions entre plusieurs parties, voir la [rubrique relative au développement d'applications](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/developing_applications.html){: external} dans la documentation Hyperledger Fabric.
- Lorsque vous être prêt(e) à commencer à générer des contrats intelligents, vous pouvez utiliser l'[extension {{site.data.keyword.blockchainfull_notm}} Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=IBMBlockchain.ibm-blockchain-platform){: external} pour commencer à générer votre propre projet de contrat intelligent. Vous pouvez également utiliser cette extension pour [vous connecter directement à votre réseau à partir de Visual Studio Code](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-vscode) et consultez les tutoriel en ligne.
- Pour un tutoriel rapide sur le développement de contrats intelligents, voir [Develop a smart contract with the IBM Blockchain Platform VS Code extension](https://developer.ibm.com/tutorials/ibm-blockchain-platform-vscode-smart-contract/){: external}.
- Pour un tutoriel de bout en bout complet sur l'utilisation d'une application pour interagir avec des contrats intelligents, voir le [tutoriel Document commercial Hyperledger Fabric](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html){: external}.
- Pour en savoir plus sur l'incorporation de mécanismes de contrôle d'accès dans votre contrat intelligent, voir le [Code blockchain pour les développeurs](https://hyperledger-fabric.readthedocs.io/en/release-1.4/chaincode4ade.html#chaincode-access-control){: external}.
- Lorsque vous êtes prêt(e) à effectuer l'installation, le contrat intelligent doit être packagé au [format .cds](https://hyperledger-fabric.readthedocs.io/en/release-1.4/chaincode4noah.html#packaging){: external} pour pouvoir être installé sur les homologues. Pour plus d'informations, voir [Packaging des contrats intelligents](/docs/services/blockchain?topic=blockchain-develop-vscode#packaging-a-smart-contract). Vous pouvez aussi utiliser les [commandes de l'interface CLI de l'homologue](https://hyperledger-fabric.readthedocs.io/en/release-1.4/commands/peerchaincode.html#peer-chaincode-package){: external} pour générer le package.
<!-- Update the tutorial link to release1-4 when it is published -->


## Etape 2 : Installer un contrat intelligent
{: #ibp-console-smart-contracts-install}

Utilisez votre console pour exécuter cette procédure :

1. Cliquez sur l'onglet **Contrats intelligents** pour installer un ou plusieurs contrats intelligents.
2. Cliquez sur **Installer un contrat intelligent** pour télécharger le fichier de contrat intelligent au [format .cds](https://hyperledger-fabric.readthedocs.io/en/release-1.4/chaincode4noah.html#packaging){: external}. _Le fichier de package de contrat intelligent doit être d'une taille inférieure à 4 Mo._ Vous pouvez utiliser l'extension {{site.data.keyword.blockchainfull_notm}} Visual Studio Code pour [créer un package de contrat intelligent](/docs/services/blockchain?topic=blockchain-develop-vscode#packaging-a-smart-contract). Lorsque vous installez le package à partir de l'onglet **Contrats intelligents**, vous pouvez sélectionner un ou plusieurs noeuds homologues sur lesquels installer les contrats intelligents.

S'il existe un seul homologue sur la console, le contrat intelligent sera installé sur celui-ci. Vous n'êtes pas invité à sélectionner un homologue pour y installer le contrat intelligent. Vous pouvez accéder à l'onglet des noeuds et cliquer sur un homologue qui est géré par la console pour afficher la liste des contrats intelligents qui ont été installés sur un homologue individuel.

Vous pouvez revenir à l'onglet **Contrats intelligents** ultérieurement pour installer le contrat intelligent sur des homologues supplémentaires, même après que le contrat intelligent a été instancié sur le canal. Si la version du contrat intelligent que vous installez est identique à la version instanciée, ces homologues supplémentaires peuvent traiter les transactions tout comme les homologues existants.
{:tip}

**Cette console ne peut pas être utilisée pour installer les fichiers `.bna` d'Hyperledger Composer.**

<!-- Instead, `.bna` files must be installed on a peer by using the [`Composer` CLI commands]("peer chaincode" "peer chaincode").  -->

## Etape 3 : Instancier un contrat intelligent
{: #ibp-console-smart-contracts-instantiate}

Les contrats intelligents sont instanciés sur un canal. Un membre de console dont les homologues ont rejoint un canal peut instancier un contrat intelligent et indiquer la [règle d'adhésion](/docs/services/blockchain?topic=blockchain-glossary#glossary-endorsement-policy) associée.

Utilisez votre console pour exécuter cette procédure :

1. Sous l'onglet des contrats intelligents, recherchez dans la liste les contrats intelligents installés sur vos homologues et cliquez sur **Instancier** dans le menu déroulant dynamique sur le côté droite de la ligne.
2. Dans le panneau latéral qui s'affiche, sélectionnez un canal sur lequel instancier le contrat intelligent. Vous pouvez sélectionner le canal, nommé `channel1`, que vous avez créé. Ensuite,
cliquez sur **Suivant**.
3. Indiquez la [règle d'adhésion pour le contrat intelligent](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-endorse), décrite dans la section ci-après. Lorsque plusieurs organisations sont membres du canal, vous avez la possibilité de choisir le nombre d'organisations qui sont nécessaires pour valider les transactions de contrat intelligent.
4. Vous devez également sélectionner les membres de l'organisation à inclure dans la règle de validation. Si vous suivez le tutoriel, il s'agit de `org1msp` et éventuellement de `org2msp` si vous avez suivi les tutoriels **Générer un réseau** et **Rejoindre un réseau**.
5. Si votre contrat intelligent comporte des collectes de données privées Fabric, vous devez envoyer par téléchargement le fichier JSON de configuration de collection associé, sinon vous pouvez omettre cette étape. Consultez cette rubrique pour plus d'informations sur l'utilisation de [données privées](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-private-data).
6. Sur le dernier panneau, vous êtes invité à spécifier la fonction de contrat intelligent que vous souhaitez exécuter au démarrage du contrat intelligent, ainsi que les arguments à transmettre à cette fonction.

Pour voir l'ensemble des contrats intelligents qui ont été instanciés sur un canal, cliquez sur l'icône de canal dans la barre de navigation de gauche, sélectionnez un canal dans la table, puis cliquez sur l'onglet **Détails du canal**.

Notez que si vous utilisez un cluster de service {{site.data.keyword.cloud_notm}} Kubernetes gratuit, l'instanciation peut être beaucoup plus longue que sur un cluster payant. Selon le nombre d'homologues que vous avez déployés dans votre cluster, cette opération peut prendre quelques minutes.

La combinaison **installation/instanciation** est une fonction puissante car elle permet à un homologue d'utiliser un seul contrat intelligent sur de nombreux canaux. Les homologues peuvent souhaiter rejoindre plusieurs canaux qui utilisent le même contrat intelligent, mais avec différents jeux de membres réseau capables d'accéder aux données. Un homologue peut installer le contrat intelligent une fois, puis utiliser le même conteneur de contrat intelligent sur un canal où il a été instancié. Cette approche permet d'éviter d'avoir à calculer l'espace de stockage, et ainsi de faire évoluer votre réseau.

## Etape 4 : Envoyer des transactions à l'aide de vos applications client
{: #ibp-console-smart-contracts-connect-to-SDK}

Une fois qu'un contrat intelligent a été instancié sur un canal, vous pouvez utiliser une application client pour effectuer des transactions avec d'autres membres de votre réseau. Les applications peuvent appeler la logique métier contenue dans les contrats intelligents pour créer, transférer ou mettre à jour des ressources sur le registre de blockchain.

### Connexion à l'aide d'un logiciel SDK
{: #ibp-console-smart-contracts-connect-to-SDK-panel}
L'onglet **Contrats intelligents** contient les informations dont vous avez besoin pour vous connecter à un contrat intelligent instancié à partir d'une application client. En regard de chaque contrat intelligent instancié, accédez au menu déroulant dynamique. Cliquez sur le bouton **Se connecter à l'aide de SDK**. Un panneau latéral s'affiche qui fournit les informations dont vous avez besoin pour vous connecter à ce contrat intelligent : nom du contrat, nom du canal et votre profil de connexion. Pour plus d'informations, voir [Création d'applications](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app).

## Indication d'une règle d'adhésion
{: #ibp-console-smart-contracts-endorse}

Chaque contrat intelligent doit avoir une règle d'adhésion, laquelle est spécifiée lors de l'instanciation. La règle d'adhésion indique l'ensemble des organisations, des homologues, sur un canal qui peut exécuter le contrat intelligent et valider de manière indépendante le résultat de la transaction. Par exemple, une règle d'adhésion peut spécifier qu'une transaction n'est ajoutée au registre que si une majorité des membres du canal la valide. L'organisation qui instancie le contrat intelligent peut sélectionner parmi les membres qui l'ont installé ceux devant faire office de valideurs et définir la règle d'adhésion pour tous les membres du canal. Vous pouvez mettre à jour votre règle d'adhésion en suivant la procédure de la rubrique relative à la [mise à jour de votre contrat intelligent](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-upgrade).

Lorsque vous suivez les étapes relatives à l'[instanciation d'un contrat intelligent](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-instantiate), vous pouvez utiliser le panneau latéral pour définir la règle d'adhésion d'un contrat une fois le canal sélectionné. Utilisez ce panneau pour spécifier une règle simple en sélectionnant les homologues qui doivent valider la transaction dans la liste des homologues ayant installé le contrat intelligent sur le canal. Vous pouvez utiliser cette méthode pour spécifier une règle d'adhésion imposant l'approbation de tous les membres du canal, d'une majorité d'entre-eux, d'un seul membre, ou simplement une règle +1 empêchant les membres de s'auto-valider. La règle d'adhésion par défaut est définie sur `1 de x`, ce qui signifie qu'un seul membre est nécessaire pour valider une transaction de contrat intelligent.

Cliquez sur le bouton **Avancé** si vous voulez indiquer une règle au format JSON. Vous pouvez utiliser cette méthode pour spécifier des règles d'adhésion plus complexes, exigeant par exemple qu'un certain membre du canal valide une transaction, ainsi qu'une majorité des autres membres. Vous pouvez trouver d'autres [exemples de règles d'adhésion](https://hyperledger-fabric.readthedocs.io/en/release-1.4/arch-deep-dive.html#example-endorsement-policies){: external} dans la documentation Hyperledger Fabric. Pour plus d'informations sur la composition de règles de validation dans JSON, reportez-vous à la [documentation du logiciel SDK Node Hyperledger Fabric](https://fabric-sdk-node.github.io/global.html#ChaincodeInstantiateUpgradeRequest){: external}.

## Mise à niveau d'un contrat intelligent
{: #ibp-console-smart-contracts-upgrade}

Vous pouvez mettre à niveau un contrat intelligent afin de modifier son code ou sa règle d'adhésion, ou sa collecte de données privées, tout en conservant sa relation aux ressources dans le registre. Vous pouvez souhaiter mettre à niveau un contrat intelligent instancié pour diverses raisons.
1. Vous pouvez mettre à niveau le contrat intelligent pour ajouter ou retirer des fonctionnalités de son code et itérer sur la logique de votre réseau métier.
2. Chaque fois qu'un nouveau membre est ajouté à un canal, la règle d'adhésion des contrats intelligents instanciés *doit* être mise à jour pour inclure le nouveau membre de canal. Pour pouvoir être utilisé avec le nouveau membre de canal, le contrat intelligent doit être repackagé avec un nouveau numéro de version et instancié sur le canal, même si le contrat intelligent lui-même reste inchangé. Sinon la validation de transaction ne peut pas aboutir.
3. Lorsqu'une collecte de données privées a changé, par exemple si une organisation est ajoutée ou retirée, vous devez mettre à niveau votre contrat intelligent. Ou bien, utilisez cette action chaque fois qu'une nouvelle collecte de données privées est ajoutée au fichier JSON de configuration de collecte.
4. Les arguments d'initialisation du contrat intelligent ont changé.

**Avant la mise à niveau d'un contrat intelligent instancié, la nouvelle version du contrat intelligent doit être installée sur tous les homologues du canal qui exécutent le niveau précédent du contrat intelligent.**

### Procédure de mise à niveau d'un contrat intelligent
{: #ibp-console-smart-contracts-upgrade-howto}

Pour mettre à niveau un contrat intelligent, installez le code mis à jour en indiquant le même nom de contrat intelligent avec un nouveau numéro de version. Si vous avez installé une version plus récente d'un contrat intelligent sur un homologue du canal, notez que la version d'origine comporte désormais le bouton `Mise à niveau disponible` dans le tableau **Contrats intelligents instanciés**.

{:important}
Lorsqu'un nouveau membre qui va exécuter le contrat intelligent rejoint le canal, il est obligatoire de mettre à jour le contrat intelligent en installant une nouvelle version sur tous les homologues et en l'instanciant sur le canal avec une règle d'adhésion modifiée qui inclut le nouveau membre.

- Accédez à l'onglet **Contrats intelligents** sur la gauche.
- Faites défiler vers le bas jusqu'au tableau **Contrats intelligents instanciés**.
- Dans le tableau **Contrats intelligents instanciés**, recherchez la version de contrat intelligent et le canal que vous voulez mettre à niveau. Il doit être suivi du libellé **Mise à niveau disponible**.
- Cliquez sur le **menu déroulant dynamique** sur le côté droit du contrat intelligent et cliquez sur **Mettre à niveau** pour effectuer les étapes suivantes :  

 1. Sélectionnez dans la liste déroulante la version de contrat intelligent que vous souhaitez mettre à niveau sur le canal.
 2. Mettez à jour la règles d'adhésion en ajoutant ou en retirant des membres de canal. Vous pouvez également cliquer sur **Avancé** pour coller une nouvelle chaîne au format JSON, qui modifie la règle existante.
 3. Si vous voulez associer le fichier de configuration d'une collecte de données privées au contrat intelligent, vous pouvez envoyer par téléchargement le fichier JSON. Ou bien, si vous voulez mise à jour une configuration de collecte existante, vous pouvez envoyer par téléchargement le fichier JSON.   
 Si le contrat intelligent a été préalablement instancié avec un fichier de configuration de collecte, vous **devez** envoyer de nouveau par téléchargement la version précédente ou une nouvelle version du fichier de configuration de collecte au cours de cette étape.  
 4. (Facultatif) Modifiez les valeurs d'argument d'initialisation de contrat intelligent si les paramètres ont changé. Si vous avez des doutes à ce sujet, vérifiez auprès du développeur de votre contrat intelligent. Si ces paramètres n'ont pas été modifiés, vous pouvez laisser cette zone vide.

Une fois que vous avez mis à niveau le contrat intelligent, vous devez modifier la version du contrat qui est instancié sur le canal, puis modifier le conteneur de contrat intelligent pour tous les homologues qui ont installé la nouvelle version. Si vous utilisez des collectes de données privées, assurez-vous d'avoir configuré des homologues d'ancrage sur le canal.

### Considérations relatives à la mise à niveau des contrats intelligents
{: #ibp-console-smart-contracts-upgrade-considerations}

1. Dois-je installer la nouvelle version du contrat intelligent sur tous mes homologues ?  

  Lorsqu'un contrat intelligent est appelé sur un homologue, il essaie d'exécuter la version qui est instanciée sur le canal. Si une version précédente est en cours d'exécution sur l'homologue, cela génère une erreur. Par conséquent, avant de mettre à niveau un contrat intelligent sur un canal, *une meilleure pratique consiste à installer la version la plus récente du contrat intelligent sur tous les homologues qui exécutent la version précédente.*  

2. Es-ce qu'une autre version de contrat intelligent peut toujours traiter les données sur le registre d'une précédente version du contrat intelligent ?  

  Oui. Dès lors que le code du nouveau contrat intelligent adresse les données en mode compatible (par l'ajout de nouvelles zones JSON et sans modifier la sémantique ou le type des zones existantes), toute version suivante du contrat intelligent peut s'exécuter sur les données d'une version précédente.

3. Que se passe-t-il si j'oublie d'effectuer une mise à niveau de mes homologues vers la dernière version avant de mettre à jour les contrats intelligents sur le canal ?  

  Après la mise à jour du canal pour l'utilisation de la nouvelle version de contrat intelligent, si des homologues du canal exécutent encore la version précédente, ils ne peuvent plus valider les transactions pour le contrat intelligent. De plus, vous risquez de ne pas avoir suffisamment de validations pour que les transactions soient validées dans le registre, selon la façon dont la règle d'adhésion de contrat intelligent est définie. Toutefois, il est possible d'installer la nouvelle version du contrat intelligent sur ces homologues ultérieurement et ils pourront de nouveau valider les transactions, avec un rattrapage efficace.

4. Que se passe-t-il si je retire une organisation de ma collecte de données privées ?

   Les homologues de cette organisation continueront à stocker des données dans la collecte de données privées jusqu'à ce que son registre atteigne le bloc qui retire son appartenance de la collecte. Lorsque cela se produit, les homologues ne reçoivent plus de données privées dans aucune transaction future, et les _clients_ de cette organisation ne peuvent plus interroger les données privées via le code blockchain d'un homologue.

## Données privées
{: #ibp-console-smart-contracts-private-data}

Les données privées sont une fonction des réseaux Hyperledger Fabric en version 1.2 ou suivante. Elles permettent de protéger la confidentialité des informations sensibles des autres membres de l'organisation **sur un canal**. La confidentialité de données s'obtient par l'utilisation de [collecte de données privées](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data/private-data.html#what-is-a-private-data-collection "Qu'est-ce qu'une collecte de données privées ?"){: external}. Par exemple, plusieurs grossistes et un groupe d'agriculteurs rejoignent un canal unique. Si un agriculteur et un grossiste souhaitent effectuer une transaction en privé, ils peuvent pour cela créer un canal. Néanmoins, ils peuvent aussi décider de créer une collecte de données privées sur le contrat intelligent qui régit leurs interactions commerciales afin de maintenir la confidentialité des aspects sensibles de la vente, comme les tarifs, sans qu'il soit nécessaire de créer un canal secondaire. Pour en savoir plus sur l'utilisation des données privées au sein d'une blockchain, consultez l'article relatif au concept de [données privées](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data/private-data.html#private-data "Données privées (Private data)"){: external} dans la documentation Fabric.

Pour pouvoir utiliser des données privées avec {{site.data.keyword.blockchainfull_notm}} Platform, il est nécessaire de remplir les trois conditions suivantes :  
1. **Définir la collecte de données privées.** Un fichier de collecte de données privées peut être ajouté à votre contrat intelligent. Ensuite, lors de l'exécution, votre application client peut utiliser des API de code blockchain spécifiques aux données privées pour entrer et extraire des données de la collecte. Pour plus d'informations sur l'utilisation de collectes de données privées avec votre contrat intelligent, consultez le tutoriel relatif au logiciel SDK Fabric dans [Using private data](https://fabric-sdk-node.github.io/tutorial-private-data.html){: external} dans la documentation Fabric SDK.  

2. **Installer et instancier le contrat intelligent.** Une fois que la collecte des données privées du contrat intelligent est définie, vous devez installer le contrat intelligent sur les homologues qui sont membres du canal. Lorsque vous instanciez un contrat intelligent sur le canal à l'aide de la console, vous devez envoyer par téléchargement le fichier JSON de configuration de collecte. Pour plus d'informations sur la [création d'un fichier JSON de définition de collecte](https://fabric-sdk-node.github.io/tutorial-private-data.html){: external}, consultez la rubrique relative aux logiciels SDK dans la documentation Fabric.

  Au lieu d'utiliser la console pour installer et instancier votre contrat intelligent avec un fichier de configuration de collecte, vous pouvez aussi utiliser le logiciel SDK Fabric. Ces instructions sont également disponibles sous [How to use private data](https://fabric-sdk-node.github.io/release-1.4/tutorial-private-data.html){: external} dans la documentation du logiciel SDK Node.  

  **Remarque :** Un client doit être un admin de votre homologue pour pouvoir installer ou instancier un contrat intelligent avec le logiciel SDK. Par conséquent, vous devez télécharger les certificats de l'identité admin de l'homologue depuis votre portefeuille de console et transmettre le certificat signataire et la clé privée de l'admin de l'homologue directement au logiciel SDK au lieu de créer une identité d'application. Pour un exemple de transmission d'une paire de clés au logiciel SDK, voir [Connexion à votre réseau à l'aide d'API de logiciel SDK Fabric de niveau inférieur](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-low-level).  


3. **Configurer des homologues d'ancrage.** Comme la communication [gossip](https://hyperledger-fabric.readthedocs.io/en/release-1.4/gossip.html){: external} entre organisations doit être activée pour que les données privées soient opérationnelles, un homologue d'ancrage doit exister pour chaque organisation dans la définition de collection. Consultez les informations relatives à la [configuration d'homologues d'ancrage](/docs/services/blockchain/howto?topic=blockchain-ibp-console-govern#ibp-console-govern-channels-anchor-peers) sur votre réseau.

Votre canal est à présent configuré pour l'utilisation des données privées.
