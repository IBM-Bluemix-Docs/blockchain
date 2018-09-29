---

copyright:
  years: 2018
lastupdated: "2018-08-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Governance della rete piano Starter
{: #getting-started-with-starter-plan}


***[Questa pagina è utile? Faccelo sapere.](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***


{{site.data.keyword.blockchainfull}} Platform piano Starter ti offre una rete blockchain preconfigurata con un singolo clic. Esegue il <!--offers you a free trial of 30 days and -->provisioning di una rete con autorizzazioni con la configurazione di due [organizzazioni](glossary.html#organization), un [peer](glossary.html#peer) per ciascuna organizzazione e un [canale](glossary.html#channel) per impostazione predefinita. Dopo che la rete è stata creata, puoi ridimensionare e aggiungere ulteriori organizzazioni e peer alla tua rete.
<!--Note that it might cause extra cost if you exceed the default resource limits of two organizations and two peers.-->
{:shortdesc}

**Nota**: {{site.data.keyword.blockchainfull}} Platform piano Starter è un ambiente di sviluppo e test  non è adatto per i carichi di lavoro di produzione. Se ti serve un ambiente di produzione, vedi [Informazioni su piano Enterprise](enterprise_plan.html).

Piano Starter ti consente di acquisire e sviluppare competenze con {{site.data.keyword.blockchainfull_notm}} Platform, eseguire applicazioni di esempio, testare le tue applicazioni e simulare uno scenario con più organizzazioni.  Questa esercitazione introduttiva presenta i prerequisiti e i passi a cui devi attenerti per creare e utilizzare una rete piano Starter.

Se non hai dimestichezza con {{site.data.keyword.blockchainfull_notm}} Platform e blockchain, puoi leggere il [Glossario](glossary.html) per familiarizzare con i termini in questa documentazione e la [documentazione di Hyperledger Fabric ![Icona link esterno](images/external_link.svg "Icona link esterno")](http://hyperledger-fabric.readthedocs.io/en/release-1.1/blockchain.html) per ulteriori informazioni sulla blockchain.


## Creazione di una rete
Puoi ottenere una [rete](glossary.html#network) piano Starter con la configurazione predefinita immediatamente dopo che hai creato un'istanza del servizio {{site.data.keyword.blockchainfull_notm}} Platform.

1. Individua il [servizio blockchain ![Icona link esterno](images/external_link.svg "Icona link esterno")](https://console.bluemix.net/catalog/services/blockchain) nel catalogo {{site.data.keyword.cloud_notm}}.   
    **Nota**: devi accedere con il tuo account a pagamento {{site.data.keyword.cloud_notm}}. Se non hai un account, fai clic sul pulsante **Registrati per creare**. Dopo aver creato un account gratuito, aggiornalo a un tipo **Pagamento a consumo** andando in **Gestisci** > **Fatturazione e utilizzo** > **Fatturazione** nella console {{site.data.keyword.cloud_notm}} e facendo clic su **Aggiungi carta di credito**.
2. Scegli la regione in {{site.data.keyword.cloud_notm}} per creare la rete.
3. Seleziona la tua organizzazione e il tuo spazio Cloud Foundry per creare la rete.
4. Scegli **Piano di appartenenza Starter** dalla tabella dei piani di prezzi.
5. Fai clic sul pulsante **Crea**. Nota: se sei invitato ad aderire a una rete, puoi vedere un pannello di benvenuto a comparsa. Per creare una rete, scegli **Procedi alla tua rete** e fai clic su **Continua**. Per aderire a una rete, vedi il passo 5 in [Adesione a una rete](#joining-a-network).
  Ora sei pronti a usare la tua rete piano Starter con la configurazione predefinita. La rete è in esecuzione con una ordinante (noto come un servizio ordini "SOLO"), due organizzazioni, una CA e un peer per ogni organizzazione. Viene anche creato un canale predefinito.
6. Fai clic sul pulsante **Avvia**.

Puoi trovare la tua istanza del servizio blockchain nel tuo [Dashboard servizio {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](images/external_link.svg "Icona link esterno")](https://console.bluemix.net/dashboard/services "{{site.data.keyword.Bluemix_notm}} dashboard servizio").


## Invio di un invito ai membri
Puoi invitare altre [organizzazioni](glossary.html#organization) ad aderire alla tua rete piano Starter come [membri](glossary.html#member) in modo da poter eseguire [transazioni](glossary.html#transaction) tra di voi. Inoltre, se vuoi usare piano Starter per finalità di apprendimento e test, puoi simulare una rete con più organizzazioni aggiungendo membri per te stesso alla rete.

1. Nella schermata "Membri" del tuo Monitoraggio della rete, fai clic sul pulsante **Invita Membri**.
2. Viene visualizzata la finestra "Invita membro".
    - Se vuoi invitare un'altra organizzazione, scegli "Invita un membro".  Specifica il nome e l'indirizzo email dell'operatore dell'organizzazione che vuoi invitare.  Puoi anche immettere le informazioni aggiuntive che vuoi includere nel tuo invito nel campo "Aggiungi una nota".  Fai clic sul pulsante **Invia invito**.  L'organizzazione invitata riceverà una email di invito e potrà quindi attenersi alle istruzioni nell'e-mail per aderire alla tua rete.
    - Se vuoi aggiungere delle ulteriori organizzazioni che possono essere aggiunte a un canale, scegli "Aggiungi un membro".  Specifica un nome per la tua nuova organizzazione. Puoi, facoltativamente, aggiungere dei peer alla tua nuova organizzazione o farlo in un secondo momento nel Monitoraggio della rete.  Fai clic sul pulsante **Crea**. Nota: se aggiungi dei peer per la tua nuova organizzazione, devi passare a questa nuova organizzazione per vedere i tuoi peer. Per ulteriori informazioni sul passaggio da un'organizzazione a un'altra, vedi [Passaggio da un'organizzazione a un'altra](dashboard.html#switch-organizations).


## Adesione a una rete
Se sei invitato da un iniziatore di rete, riceverai una notifica email con le istruzioni su come aderire alla rete. Attieniti alle istruzioni nell'email e diventerai uno dei membri nella rete.

Devi creare un'istanza del servizio [{{site.data.keyword.blockchain}} Platform ![Icona link esterno](images/external_link.svg "Icona link esterno")](https://console.bluemix.net/catalog/services/blockchain) con l'opzione di adesione piano Starter in {{site.data.keyword.cloud_notm}}.

1. Accedi con il tuo account {{site.data.keyword.cloud_notm}}. Se non hai un account, fai clic sul pulsante **Registrati per creare**.
2. Seleziona l'organizzazione Cloud Foundry dove vuoi memorizzare la tua rete {{site.data.keyword.blockchain}}.
3. Seleziona **Piano di appartenenza Starter** dalla tabella dei piani di prezzi.
4. Fai clic sul pulsante **Crea**. La pagina dell'istanza del servizio si apre con un pannello di benvenuto a comparsa. Nota: puoi scegliere di aderire a una rete o continuare a crearne una tua. Per creare una rete, vedi il passo 4 in [Creazione di una rete](#creating-a-network).
5. Nel pannello di benvenuto, scegli **Unisciti a una rete esistente**, seleziona la rete a cui aderire dall'elenco a discesa e fai clic su **Continua**.

Puoi trovare la tua istanza del servizio blockchain nel dashboard del servizio [{{site.data.keyword.cloud_notm}} ![Icona link esterno](images/external_link.svg "Icona link esterno")](https://console.bluemix.net/dashboard/services "{{site.data.keyword.cloud_notm}} - dashboard del servizio").

<!--
## Creating channels
You can create a [channel](glossary.html#channel) in your network and invite other organizations to your channel.  For more information on creating channels, see [Creating a channel](howto/create_channel.html#creating-a-channel).
-->
<!--
## Installing and instantiating your chaincode
You can run [chaincode](glossary.html#chaincode) on your peers in the network.  For more information about deploying pre-built samples, see [Installing, instantiating, and updating a chaincode](howto/install_instantiate_chaincode.html).
-->


## Richiamo delle credenziali di rete e profilo di connessione
Dopo che hai creato una rete piano Starter in {{site.data.keyword.cloud_notm}}, puoi richiamare le credenziali di rete e il profilo di connessione dalla pagina dell'istanza del servizio oppure nel Monitoraggio della rete.

### Richiamo dalla pagina dell'istanza del servizio
Sei nella pagina dell'istanza del servizio subito dopo aver creato un'istanza del servizio. Puoi anche fare clic sul tuo servizio nel [dashboard del servizio {{site.data.keyword.cloud_notm}} ![Icona link esterno](images/external_link.svg "Icona link esterno")](https://console.bluemix.net/dashboard/services "{{site.data.keyword.cloud_notm}} - dashboard del servizio") per aprire la tua pagina dell'istanza del servizio.

Richiama le tue credenziali del servizio attenendoti alla seguente procedura:
1. Nella pagina dell'istanza del servizio, fai clic su **Credenziali del servizio** nel navigatore a sinistra per visualizzare la schermata "Credenziali del servizio".
2. Fai clic su **Nuova credenziale** nella schermata "Credenziali del servizio".
3. Nella schermata "Aggiungi nuova credenziale", dai un nome alla credenziale e immetti **{"type": "service_instance_token"}** nel campo "Aggiungi parametro di configurazione inline". Fai clic su **Aggiungi**. La nuova credenziale viene aggiunta nella tabella. Puoi fare clic su **Visualizza credenziali** nella colonna "AZIONI" per visualizzare i dettagli della credenziale. Questa credenziale contiene la chiave API e il segreto, che puoi utilizzare per autorizzare le API.  

![Richiamo delle credenziali della rete](images/service_credentials.gif "Richiamo delle credenziali della rete")

### Richiamo nel Monitoraggio della rete
Puoi trovare le credenziali di rete sulla schermata "API" nel tuo Monitoraggio della rete. Per ulteriori informazioni sull'utilizzo delle API, vedi [Interazione con la rete utilizzando le API Swagger](howto/swagger_apis.html).

Puoi richiamare il profilo di connessione nella schermata "Panoramica" nel tuo Monitoraggio della rete. Fai clic sul pulsante **Profilo connessione** nella schermata "Panoramica"; il profilo di connessione viene visualizzato in una nuova pagina.


## Distribuzione di applicazioni di esempio
Piano Starter ti consente di distribuire delle applicazioni di esempio alla tua rete con solo pochi clic. Con gli esempi, puoi facilmente imparare la modalità di funzionamento di chaincode e applicazioni in una rete.

Per ulteriori informazioni, vedi [Distribuzione di applicazioni di esempio](howto/prebuilt_samples.html).


## Sviluppo e distribuzione di reti di business personalizzate
Il piano Starter integra l'ambiente per sviluppatori {{site.data.keyword.blockchainfull_notm}} Platform: Develop e il set di strumenti per gli sviluppatori Hyperledger Composer. Puoi sviluppare la tua rete blockchain in base alle tue esigenze di business.  Dopo che hai sviluppato una rete per il tuo business, puoi distribuire la tua rete di business nella rete piano Starter.

Per ulteriori informazioni, vedi [Sviluppare la rete](develop.html) e [Distribuzione delle reti di business con piano Starter](develop_starter.html).


## Monitoraggio delle risorse di rete
Se la tua applicazione richiede una transazione, puoi visualizzare le informazioni sullo stato della transazione nel Monitoraggio della rete. Per ulteriori informazioni sul monitoraggio di rete, vedi [Monitoraggio di una rete](howto/monitor_network.html).


## Reimpostazione di una rete
Se vuoi cancellare le tue configurazioni personalizzate, la tua chaincode in esecuzione o le tue applicazioni distribuite, puoi impostare nuovamente la tua rete sulla configurazione predefinita iniziale.  Per ulteriori informazioni, vedi [Reimpostare la rete](dashboard.html#reset-network).


## Migrazione dal piano Starter al piano Enterprise
{: #migrate}

Puoi distribuire in una rete piano Enterprise un `.bna`, chaincode e applicazioni di cui esegui il test su una rete piano Starter.

Se hai un tuo file di archivio di rete di business (`.bna`), attieniti alle istruzioni per la [distribuzione di una rete di business al piano Enterprise](./develop_enterprise.html). Se non hai un tuo file `.bna`, usa il comando `composer network download` per richiamarlo dall'istanza del piano Starter. Per ulteriori informazioni sul comando `composer network download`, vedi la [documentazione della riga di comando Hyperledger Composer ![Icona link esterno](images/external_link.svg "Icona link esterno")](https://hyperledger.github.io/composer/latest/reference/commands){:new_window}.

Il chaincode, che è simile ai file `.bna`, è sviluppato esternamente. Per distribuire in Enterprise un chaincode di cui esegui il test su una rete piano Starter, attieniti alle istruzioni in [Installazione, istanziazione e aggiornamento di un chaincode](howto/install_instantiate_chaincode.html#installchaincode).

<!--
As you can see in [Deploying sample applications](howto/prebuilt_samples.html), Starter Plan makes it easy to get a sample application integrated with your network by using Toolchain. This setup also allows for continuous integration by automatically updating your sample application whenever your forked application repo is changed. If you want to deploy this application into an Enterprise Plan network, you can copy your forked application repo into a new repo and then follow the instructions in [Deploying sample applications manually](howto/prebuilt_samples.html#deploy_sample_applications_manually).
-->

Se distribuisci una qualche applicazione di esempio nella tua rete piano Starter e vuoi distribuire questa applicazione in una rete piano Enterprise, puoi copiare il tuo repository di applicazioni duplicato in un nuovo repository e attenerti quindi alle istruzioni nelle applicazioni di esempio per eseguirne la distribuzione sulla tua rete piano Enterprise.


## Eliminazione, o uscita da, una rete
Se vuoi eliminare, o uscire da, una rete, puoi eliminare l'istanza del servizio blockchain dal tuo dashboard {{site.data.keyword.cloud_notm}}.

**Nota**: prima di uscire da una rete, assicurati di non essere un membro dei canali della rete. Altrimenti, riscontrerai degli errori quando esci dalla rete. Una rimozione di un membro del canale deve completare il processo di aggiornamento del canale. Per ulteriori informazioni sul processo di aggiornamento del canale, consulta [Aggiornamento di un canale](howto/create_channel.html#updating-a-channel).


<!--
## References
* For more information about {{site.data.keyword.blockchainfull_notm}} offerings, see [Blockchain offerings](index.html).
* For more information about Hyperledger Fabric V1.1, see [Hyperledger Fabric documentation ![External link icon](images/external_link.svg "External link icon")](http://hyperledger-fabric.readthedocs.io/en/release-1.1/){:new_window}.
-->
