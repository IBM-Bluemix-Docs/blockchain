---

copyright:
  years: 2019
lastupdated: "2019-06-18"

keywords: IBM Blockchain Platform console, administer a console, add users, remove users, modify a user's role, install patches, Kubernetes cluster expiration

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
{:gif: data-image-type='gif'}


# Administration de votre console
{: #ibp-console-manage-console}

Vous pouvez gérer le comportement de votre console de plusieurs manières. Cette rubrique décrit des actions autres que les opérations de noeud de blockchain qui vous aident dans votre usage quotidien de la console.
{:shortdesc}

**Public cible :** Cette rubrique s'adresse aux opérateurs réseau qui sont responsables de la création, de la surveillance et de la gestion du réseau de blockchain.

## Ajout et retrait d'utilisateurs de la console
{: #ibp-console-manage-console-add-remove}

Chaque utilisateur qui accède à la console doit se voir attribuer une règle d'accès pour laquelle un rôle utilisateur IAM ({{site.data.keyword.cloud}} Identity and Access Management) est défini. La règle détermine les actions que l'utilisateur peut effectuer sur la console. La console {{site.data.keyword.blockchainfull_notm}} Platform est accessible avec l'adresse e-mail du propriétaire {{site.data.keyword.cloud_notm}} en tant qu'administrateur de la console.  Par défaut, cet utilisateur {{site.data.keyword.cloud_notm}} se voit accorder le rôle **Gestionnaire** pour le service {{site.data.keyword.blockchainfull_notm}} Platform dans IAM. L'administrateur de console peut ensuite accorder l'accès de la console à d'autres utilisateurs à partir de l'interface utilisateur IAM. Pour plus d'informations sur IAM, voir [Qu'est-ce qu'IAM ?](/docs/iam?topic=iam-iamoverview#iamoverview){: external}.  

Lorsque vous [utilisez IAM pour inviter des utilisateurs](/docs/iam?topic=iam-iamuserinv#iamuserinv){: external}, vous devez procéder comme suit pour configurer leurs rôles et leur accès à la console :
 1. Dans la barre de menus, cliquez sur **Gérer** > **Accès (IAM)**, puis sélectionnez **Utilisateurs**.
 2. Cliquez sur **Inviter un utilisateur**.
 3. Entrez l'adresse e-mail du ou des utilisateurs.
 4. Dans la liste déroulante **Services**, sélectionnez **Blockchain Platform**.
 5. Faites défiler jusqu'à **Sélectionner des rôles**.
 6. Sous **Affecter des rôles d'accès à un service**, choisissez un rôle pour l'utilisateur, qui peut être **Gestionnaire**, **Auteur** et **Lecteur**.
 7. Cliquez sur **Inviter des utilisateurs**.

| Rôle | Fonctions |
|--------|----------|
| Gestionnaire | En tant que Gestionnaire, vos droits vont au-delà de ceux du rôle Auteur. Vous pouvez faire tout ce que peut faire un Lecteur et un Auteur ainsi que les opérations suivantes : <ul><li>Mettre à disposition de nouveaux composants à l'aide de la console ou d'API.</li><li>Supprimer des composants mis à disposition à l'aide de la console ou d'API.</li><li>Modifier les niveaux de consignation de la console à l'aide de la console ou d'API.</li><li>Redémarrer la console à l'aide d'une API.</li></ul> |
| Auteur | En tant que Auteur, vos droits vont au-delà de ceux du rôle Lecteur, notamment : <ul><li>Importer des composants à l'aide de la console ou d'API.</li><li>Supprimer des composants importés à l'aide de la console ou d'API.</li><li>Enregistrer des utilisateurs auprès d'une autorité de certification.</li><li> Ajouter ou supprimer des notifications à l'aide de la console ou d'API.</li></ul>  |
| Lecteur | En tant que Lecteur, vous pouvez effectuer des actions en lecture seule, et notamment : <ul><li>Afficher l'interface utilisateur de la console.</li><li>Consulter le journal de la console.</li><li>Exporter des composants.</li><li>Emettre une API GET.</li></ul> | |

 Les droits d'accès sont cumulatifs. Si vous choisissez un rôle **Gestionnaire**, l'utilisateur pourra également effectuer toutes les actions des rôles **Auteur** et **Lecteur**, vous n'avez donc pas à sélectionner également ces rôles.   De même, un utilisateur avec le rôle `Auteur` pourra effectuer toutes les actions du rôle **Lecteur**. Pour l'accès à la console, il vous suffit de sélectionner un rôle sous **Rôles d'accès au service**, vous n'avez rien à sélectionner sous **Rôles d'accès à une plateforme**. Sélectionnez le rôle correspondant sous **Affecter des rôles d'accès à une plateforme** s'il est important que l'instance de service soit visible dans le tableau de bord {{site.data.keyword.cloud_notm}} de l'utilisateur invité.

![Ajout d'utilisateurs](../images/AddICPUser.gif){: gif}


Après que vous avez ajouté de nouveaux utilisateurs à la console, il se peut que ceux-ci ne puissent pas voir l'ensemble des noeuds, canaux ou codes blockchain, déployés par d'autres utilisateurs. Pour pouvoir gérer ces composants, chaque utilisateur doit importer les identités associées dans son propre portefeuille de console. Pour plus d'informations, voir [Stockage des identités dans votre portefeuille de console](/docs/services/blockchain/howto?topic=blockchain-ibp-console-identities#ibp-console-identities-wallet).
{:important}

Si vous devez modifier le rôle d'un utilisateur :
 1. Dans la barre de menus, cliquez sur **Gérer** > **Accès (IAM)**, puis sélectionnez **Utilisateurs**.
 2. Cliquez sur le menu Actions en regard de l'utilisateur que vous voulez modifier et sélectionnez **Affecter un accès**.
 3. Sélectionnez la vignette **Affecter l'accès aux ressources**.
 4. Dans la liste déroulante **Services**, sélectionnez **Blockchain Platform 2.0**.
 5. Faites défiler jusqu'à **Sélectionner des rôles**.
 6. Sous **Affecter des rôles d'accès à un service**, choisissez un rôle pour l'utilisateur, qui peut être **Gestionnaire**, **Auteur** et **Lecteur**.
 7. Cliquez sur **Affecter**.

SI vous devez retirer l'accès d'un utilisateur à la console, suivez les instructions de la section [IAM Removing users](/docs/iam?topic=iam-remove#remove){: external}.

### Affectation de rôles d'accès à des utilisateurs individuels ou à des groupes d'utilisateurs dans IAM
{: #ibp-console-manage-console-users-groups}

Lorsque vous définissez des règles {{site.data.keyword.cloud_notm}} IAM, vous pouvez affecter des rôles à un utilisateur individuel ou à un groupe d'utilisateurs.

<dl>
<dt>Utilisateurs individuels</dt>
<dd>Vous pouvez disposer d'un utilisateur nécessitant plus ou moins de droits que le reste de votre équipe. Vous pouvez personnaliser les droits d'accès sur une base individuelle de sorte que chaque personne dispose des droits dont elle a besoin pour accomplir sa tâche. Vous pouvez affecter plusieurs rôles {{site.data.keyword.cloud_notm}} IAM à chaque utilisateur.</dd>
<dt>Plusieurs utilisateurs au sein d'un groupe d'accès</dt>
<dd>Vous pouvez créer un groupe d'utilisateurs et affecter des droits d'accès à ce groupe. Par exemple, vous pouvez regrouper tous les chefs d'équipe et affecter l'accès administrateur à ce groupe. Vous pouvez ensuite regrouper tous les développeurs et affecter uniquement les droits d'accès en écriture à ce groupe. Vous pouvez affecter plusieurs rôles {{site.data.keyword.cloud_notm}} IAM à chaque groupe d'accès. Lorsque vous affectez des droits à un groupe, tous les utilisateurs ajoutés ou retirés dans ce groupe sont impactés. Si vous ajoutez un utilisateur dans le groupe, il dispose également de cet accès supplémentaire. S'il est supprimé, son accès est révoqué.</dd>
</dl>

Les utilisateurs que vous ajoutez dans IAM sont simplement les adresses e-mail des utilisateurs qui peuvent se connecter à la console. Ils n'ont aucune relation avec les **Organisations disponibles** dans l'onglet Organisations ou avec les identités stockées par le portefeuille de console.
{:note}

## Mise à jour de l'adresse e-mail de l'administrateur

Si la console est utilisée par plusieurs personnes ou organisations, il est recommandé de créer une adresse e-mail fonctionnelle pour accéder à votre réseau. Cette adresse e-mail vous permettra d'accéder à la console si l'admin d'origine quitte votre organisation ou encore si son adresse e-mail est suspendue. Une seule adresse e-mail peut être utilisée en tant que contact administrateur.

Pour pouvoir mettre à jour l'adresse e-mail de l'administrateur de console qui a été configurée lors du déploiement de la console, vous devez être connecté en tant qu'administrateur de console. Accédez à l'onglet **Utilisateurs** et cliquez sur **Configurer** sur la vignette **{{site.data.keyword.IBM_notm}}ID**. Dans le panneau qui s'affiche, indiquez une nouvelle adresse e-mail pour l'administrateur de la console.

## Consultation des journaux
{: #ibp-console-manage-logs}

Lors de l'utilisation de la console {{site.data.keyword.blockchainfull_notm}} Platform, vous devrez peut-être consulter les journaux afin de déboguer un problème.

### Consultation des journaux de la console
{: #ibp-console-manage-console-logs}

Vous pouvez facilement accéder aux journaux de la console si vous avez besoin de déboguer des problèmes que vous rencontrez lors de l'utilisation de la console ou de l'exploitation de vos noeuds. Vous pouvez également définir le niveau de consignation afin d'augmenter ou de diminuer le nombre de journaux collectés par la console. Les journaux de la console sont collectés séparément des [journaux de vos noeuds](/docs/services/blockchain/howto?topic=blockchain-ibp-console-manage-console#ibp-console-manage-console-node-logs), lesquels sont collectés par le service {{site.data.keyword.cloud_notm}} Kubernetes.

Accédez à l'onglet **Paramètres** dans le navigateur de la console pour modifier les paramètres de journalisation. Les journaux de la console sont collectés à partir de deux sources distinctes :

  * **Journalisation client :** Ces journaux sont collectés lorsque des commandes sont envoyées depuis votre navigateur à la console.
  * **Journalisation serveur :** Ces journaux sont collectés lorsque la console envoie des commandes à vos noeuds et depuis le déploiement de la console. Ils incluent la sortie de journalisation d'Hyperledger Fabric.

Définissez le nombre de journaux collectés dans la liste déroulante sous chaque type de journal. Par exemple, **Erreur** et **Avertissement** correspondent à la collecte de journaux la moins élevée, tandis que **Débogage** et **Tout** correspondent à la collecte de journaux la plus élevée.

Vous pouvez afficher uniquement les journaux de la console si vous êtes connecté en tant qu'administrateur de console. Pour afficher les journaux depuis l'onglet **Paramètres**, remplacez le mot `settings` dans l'URL du navigateur par `api/v1/logs`. Par exemple, si l'URL de votre console est `localhost:3001/settings`, vous pouvez consulter vos journaux en accédant à l'adresse `localhost:3001/api/v1/logs`. Les journaux client et serveur sont collectés dans des fichiers distincts. Les journaux les plus récents figurent en haut de la page.

### Consultation des journaux de votre noeud
{: #ibp-console-manage-console-node-logs}

Les journaux de vos homologues, noeuds de tri et autorités de certification sont collectés par le service {{site.data.keyword.IBM_notm}} Kubernetes. Utilisez les étapes ci-dessous pour consulter les journaux de vos noeuds depuis le cluster où vous avez déployé votre réseau {{site.data.keyword.blockchainfull_notm}} Platform.

Pour localiser plus facilement les journaux de votre noeud, il est recommandé de filtrer sur l'espace de nom qui a été utilisé lors du déploiement des noeuds. Pour trouver l'espace de nom, ouvrez le noeud de votre autorité de certification et cliquez sur l'icône **Paramètres**. Affichez la valeur de l'**URL de noeud final de l'autorité de certification**. Par exemple : `https://n2734d0-paorg10524.ibpv2-cluster.us-south.containers.appdomain.cloud:7054`.

L'espace de nom est la première partie de l'URL commençant par la lettre `n` et suivie d'une chaîne aléatoire de six caractères alphanumériques. Ainsi, dans l'exemple ci-dessus, la valeur de l'espace de nom est `n2734d0`.

1. Ouvrez le tableau de bord [{{site.data.keyword.cloud_notm}} ](https://cloud.ibm.com/resources){: external} et accédez à l'écran de présentation de votre cluster {{site.data.keyword.IBM_notm}} Kubernetes Service.
2. Au-dessus de l'écran de présentation, cliquez sur **Tableau de bord Kubernetes**.
3. Dans le tableau de bord Kubernetes, utilisez la liste déroulante **Espace de nom** pour modifier l'espace de nom de l'instance de service {{site.data.keyword.blockchainfull_notm}} Platform que vous avez découverte ci-dessus.
4. Dans la navigation de gauche, cliquez sur **Pods** pour afficher la liste des pods de noeud que vous avez déployés.
5. Cliquez sur un pod. Cliquez ensuite sur **Journaux** dans le menu du haut pour ouvrir les journaux de votre noeud. Au-dessus des journaux, vous pouvez utiliser le menu déroulant en regard de **Journaux de ** pour consulter les journaux des différents conteneurs au sein du pod. Par exemple, votre homologue et la base de données d'état (CouchDB, par exemple) s'exécutent dans des conteneurs différents et génèrent des journaux différents.

Par défaut, les journaux de vos noeuds sont collectés en local au sein de votre cluster. Vous pouvez également utiliser les services {{site.data.keyword.cloud_notm}} ou un service tiers pour collecter, stocker et analyser les journaux de votre réseau. Pour plus d'informations, voir [Logging and monitoring for the {{site.data.keyword.IBM_notm}} Kubernetes Service](/docs/containers?topic=containers-health#health){: external}. Nous vous recommandons d'utiliser le service [{{site.data.keyword.cloud_notm}} LogDNA](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-kube#kube){: external} qui vous permet d'analyser facilement les journaux en temps réel.

### Consultation des journaux de votre conteneur de contrat intelligent
{: #ibp-console-manage-console-container-logs}

Si vous rencontrez des problèmes au niveau de votre contrat intelligent, vous pouvez consulter les journaux du conteneur de contrat intelligent, ou de code blockchain, pour déboguer un problème :

- Ouvrez votre tableau de bord Kubernetes, filtrez sur votre [espace de nom](#ibp-console-manage-console-node-logs), puis cliquez sur le pod homologue dans lequel s'exécute le contrat intelligent.
- Cliquez sur le lien `Journaux` depuis votre tableau de bord. Par défaut, il pointe sur le conteneur homologue.
- Basculez vers le conteneur `fluentd` en le sélectionnant dans la liste déroulante.  

Les journaux de tous vos contrats intelligents sont visibles dans cette fenêtre et ils peuvent être téléchargés à l'aide de l'icône de téléchargement sur le panneau.

## Installation de correctifs pour vos noeuds
{: #ibp-console-manage-patch}

Les images docker {{site.data.keyword.IBM_notm}} Hyperledger Fabric sous-jacentes pour les noeuds de l'homologue, de l'autorité de certification et des noeuds de tri devront peut-être mis à jour, par exemple, avec des mises à jour de sécurité ou pour une nouvelle édition de point Fabric. Le texte **Correctif disponible** dans le titre d'une vignette indique qu'un correctif est disponible et peut être installé sur le noeud dès que vous êtes prêt(e). Ces correctifs sont facultatifs, mais recommandés.  Vous ne pouvez pas appliquer des correctifs à des noeuds qui sont importés sur la console.

Les correctifs sont appliqués à tous les noeuds en même temps. Lorsque le correctif est appliqué, le noeud n'est pas disponible pour traiter des demandes ou des transactions. Par conséquent, pour éviter toute interruption de service, vous devez vérifier chaque fois que possible qu'un autre noeud du même type est disponible pour le traitement des demandes. L'installation de correctifs sur un noeud prend environ une minute et une fois la mise à jour terminée, le noeud est prêt à traiter des demandes.
{:note}

Pour appliquer un correctif sur un noeud, ouvrez la vignette du noeud et cliquez sur le bouton **Installer un correctif** . Vous ne pouvez pas appliquer des correctifs à des noeuds que vous avez importés sur la console.

## Expiration du cluster Kubernetes
{: #ibp-console-manage-console-cluster-expiration}

Si vous utilisez un cluster {{site.data.keyword.cloud_notm}} Kubernetes Service gratuit, il expirera au bout de 30 jours. Lorsque cela se produit, vous ne pouvez plus accéder à votre console. Tous les noeuds et les certificats associés sont également supprimés. Vous ne pouvez avoir qu'un seul cluster gratuit à la fois. Par conséquent, avant de créer une autre instance de service blockchain, vous devez vous assurer que le cluster expiré et son instance de service associée ont été supprimés de {{site.data.keyword.cloud_notm}}. Pour confirmer qu'ils sont déjà été supprimés ou pour supprimer manuellement ces ressources, procédez comme suit :

1. Sur votre tableau de bord {{site.data.keyword.cloud_notm}}, cliquez sur le menu latéral et ouvrez la **Liste de ressources**.
2. Faites défiler jusqu'au bouton de développement **Services** et développez-le pour afficher votre instance de service.
3. Si votre instance est répertoriée, cliquez sur le menu Action de l'instance de service, puis sur **Supprimer**, afin de supprimer cette instance de service.
4. Faites défiler jusqu'au bouton de développement **Clusters Kubernetes** et développez-le pour afficher votre cluster gratuit.
5. Si votre cluster gratuit est répertorié, cliquez sur le menu Action du cluster, puis sur **Supprimer**, afin de supprimer le cluster gratuit.

Lorsque ces actions sont terminées, vous pouvez suivre les [étapes d'origine](/docs/services/blockchain/howto?topic=blockchain-ibp-v2-deploy-iks#ibp-v2-deploy-iks) pour créer un nouveau cluster Kubernetes et une instance de service blockchain depuis la page de catalogue {{site.data.keyword.cloud_notm}}.
