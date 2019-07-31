---

copyright:
  years: 2019
lastupdated: "2019-06-18"

keywords: client application, Commercial Paper, SDK, wallet, generate a certificate, generate a private key, fabric gateway, APIs, smart contract

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

# Creazione di applicazioni
{: #ibp-console-app}

Dopo aver installato gli smart contract e distribuito i tuoi nodi, puoi utilizzare le applicazioni client per effettuare transazioni con gli altri membri della tua rete. Le applicazioni possono richiamare la logica di business contenuta negli smart contract per creare, trasferire o aggiornare gli asset nel libro mastro blockchain. Utilizza questa esercitazione per imparare ad utilizzare le applicazioni client per interagire con le reti che gestisci dalla console {{site.data.keyword.blockchainfull}} Platform.
{:shortdesc}

**Gruppi di destinatari:** questo argomento è pensato per gli sviluppatori dell'applicazione che sono interessati ad avere ulteriori informazioni su come creare un'applicazione client che interagisce con una rete blockchain.

## Risorse di apprendimento
{: #ibp-console-app-learning-resources}

Puoi scoprire di più su come applicazioni e smart contract lavorano insieme nell'esempio di Commercial Paper. Visita l'argomento [Esegui l'esempio della commercial paper su {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-commercial-paper)| dove puoi scoprire come distribuire e richiamare il contratto della commercial paper.

Lo sviluppo di un'applicazione potrebbe richiedere il coordinamento tra due utenti distinti della tua rete, l'operatore di rete e lo sviluppatore di applicazioni:
- **L'operatore di rete** è l'amministratore che utilizza la console {{site.data.keyword.blockchainfull_notm}} Platform per distribuire i nodi della tua organizzazione e installa gli smart contract sulla tua rete.
- **Lo sviluppatore di applicazioni** crea l'applicazione client che verrà utilizzata dagli utenti finali. Lo sviluppatore utilizza gli [SDK Hyperledger Fabric](https://hyperledger-fabric.readthedocs.io/en/release-1.4/getting_started.html#hyperledger-fabric-sdks){: external} per richiamare le transazioni scritte negli smart contract.

Se sei l'**operatore di rete**, dovrai completare i seguenti passi prima che lo sviluppatore di applicazioni possa interagire con la tua rete.
1. Utilizza la CA della tua organizzazione per [registrare un'identità dell'applicazione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-identities).
2. [Scarica il profilo di connessione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-profile) dal pannello degli smart contract.
3. Invia allo sviluppatore di applicazioni i seguenti oggetti e informazioni:
  - L'ID e il segreto di iscrizione dell'identità dell'applicazione.
  - Il profilo di connessione.
  - Il nome dello smart contract.
  - Il nome del canale in cui è stato istanziato lo smart contract.  

Se sei lo **sviluppatore di applicazioni**, utilizza le informazioni fornite dall'operatore di rete per completare i seguenti passi:
1. Genera un certificato e una chiave privata utilizzando l'ID e il segreto di iscrizione dell'identità dell'applicazione, insieme alle informazioni sull'endpoint CA all'interno del tuo profilo di connessione.
2. Utilizza il profilo di connessione, il nome del canale, il nome dello smart contract e le chiavi dell'applicazione per richiamare lo smart contract.  

Il profilo di connessione scaricato dalla console {{site.data.keyword.blockchainfull_notm}} Platform può essere utilizzato solo per la connessione alla tua rete utilizzando gli SDK Node.js (JavaScript e TypeScript) e Java Fabric.
{: note}

Lo sviluppatore di applicazioni può utilizzare due modelli di programmazione per interagire con la rete:

**API SDK Fabric di alto livello**

A partire da Fabric v1.4, gli utenti possono usufruire di un modello di programmazione di applicazioni e smart contract semplificato. Il nuovo modello riduce il numero di passi e la quantità di codice necessari per inviare una transazione. Questo modello è supportato solo per le applicazioni scritte in **Node.js**. Se vuoi usufruire del nuovo modello, puoi utilizzare questa esercitazione per completare le seguenti azioni su una rete {{site.data.keyword.blockchainfull_notm}} Platform.

- [Genera certificati per la tua applicazione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-enroll) utilizzando l'SDK.
- [Richiama uno smart contract dall'SDK](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-invoke).
- Acquisisci informazioni sullo sviluppo di applicazioni distribuendo l'[esercitazione sulla commercial paper](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-commercial-paper) ai nodi gestiti dalla tua console. Questa esercitazione fornirà un ulteriore background su come utilizzare i portafogli e i gateway Fabric.

**API SDK Fabric di basso livello**

Se vuoi continuare a utilizzare il tuo codice di smart contract e applicazioni esistente o vuoi utilizzare gli altri linguaggi SDK Fabric forniti dalla community Hyperledger, puoi usare le [API SDK Fabric di basso livello](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-low-level) per connetterti alla tua rete.

## Registrazione di un'identità dell'applicazione
{: #ibp-console-app-identities}

Le applicazioni devono firmare le transazioni che inviano ai nodi {{site.data.keyword.blockchainfull_notm}} e allegare un certificato di firma utilizzato dai nodi per verificare che le transazioni vengano inviate dalla parte corretta. Ciò garantisce che le transazioni vengano inviate dalle organizzazioni autorizzate a partecipare.

L'operatore di rete deve utilizzare la CA dell'organizzazione per [registrare un'identità dell'applicazione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-identities#ibp-console-identities-register), che può quindi essere utilizzata dallo sviluppatore di applicazioni per generare un certificato e una chiave privata. L'operatore può fornire l'ID e il segreto di iscrizione dell'identità, insieme alle informazioni sull'endpoint CA, che verranno utilizzati dall'SDK per generare i certificati. Effettuando l'iscrizione sul lato client, lo sviluppatore di applicazioni garantisce che nessun'altra parte abbia accesso alla chiave privata dell'applicazione. Durante la registrazione, l'operatore di rete può impostare un limite di iscrizione di uno per ulteriore sicurezza. Dopo che lo sviluppatore di applicazioni esegue l'iscrizione, non è possibile utilizzare l'ID e il segreto di iscrizione per generare un'altra chiave privata.

Se non sei molto preoccupato per la sicurezza, l'operatore di rete può iscrivere un'identità dell'applicazione utilizzando la [scheda CA](/docs/services/blockchain/howto?topic=blockchain-ibp-console-identities#ibp-console-identities-enroll). L'operatore può quindi scaricare l'identità o esportarla nel portafoglio della console. Per utilizzare i certificati dall'SDK, le chiavi devono essere decodificate dal formato base64 in formato PEM. Puoi decodificare i certificati immettendo il seguente comando sulla tua macchina locale:

```
export FLAG=$(if [ "$(uname -s)" == "Linux" ]; then echo "-w 0"; else echo "-b 0"; fi)
echo <base64_string> | base64 --decode $FLAG > <key>.pem
```
{:codeblock}

## Scaricamento del tuo profilo di connessione
{: #ibp-console-app-profile}

Le applicazioni sono in grado di inviare transazioni solo agli smart contract che sono stati istanziati sui canali. Di conseguenza, le informazioni che devi connettere per interagire con uno smart contract possono essere trovate nell'elenco degli smart contract istanziati nella tua console. Ciò significa che devi aver già installato e istanziato il tuo smart contract.

Il profilo di connessione scaricato dalla console {{site.data.keyword.blockchainfull_notm}} Platform può essere utilizzato solo per la connessione alla tua rete utilizzando gli SDK Node.js (JavaScript e TypeScript) e Java Fabric.
{: note}

Il [flusso di transazioni](https://hyperledger-fabric.readthedocs.io/en/release-1.4/txflow.html){: external} di Hyperledger Fabric si estende a più componenti, dove le applicazioni client raccolgono le approvazioni dai peer e inviano le transazioni approvate al servizio ordini. Il profilo di connessione fornisce alla tua applicazione gli endpoint dei peer e i nodi di ordine di cui ha bisogno per inviare una transazione. Contiene inoltre informazioni sulla tua organizzazione, come le tue autorità di certificazione (CA) e il tuo ID MSP. Gli SDK Fabric possono leggere direttamente il profilo di connessione, senza dover scrivere il codice che gestisce il flusso di transazione e di approvazione.

Per poterti avvalere della funzione di [rilevamento dei servizi](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html){: external} di Hyperledger Fabric, devi configurare i peer di ancoraggio. Il rilevamento dei servizi consente alla tua applicazione di conoscere quali peer sul canale esterno alla tua organizzazione devono approvare una transazione. Senza il rilevamento dei servizi, dovrai ottenere le informazioni sugli endpoint di questi peer fuori banda da altre organizzazioni e aggiungerle al tuo profilo di connessione. Per ulteriori informazioni, vedi [Configurazione di peer di ancoraggio](/docs/services/blockchain/howto?topic=blockchain-ibp-console-govern#ibp-console-govern-channels-anchor-peers).

Passa alla scheda **Smart contracts** nella tua console della piattaforma. Accanto a ciascuno smart contract istanziato, vai al menu di overflow. Fai clic sul pulsante denominato **Connettiti con SDK**. Verrà aperto un pannello laterale che ti consentirà di creare e scaricare il tuo profilo di connessione. Innanzitutto, devi selezionare la CA della tua organizzazione che hai utilizzato per registrare l'identità della tua applicazione. Dovrai anche selezionare la definizione di MSP della tua organizzazione. Sarai quindi in grado di scaricare il profilo di connessione che puoi utilizzare per generare i certificati e richiamare lo smart contract.

Se i tuoi nodi vengono distribuiti a {{site.data.keyword.cloud_notm}} Private, devi garantire che le porte utilizzate da autorità di certificazione (CA), peer e ordinanti nel profilo di connessione siano esposte esternamente alle tue applicazioni client.
{: note}


## Iscrizione utilizzando l'SDK
{: #ibp-console-app-enroll}

Una volta che l'operatore di rete fornisce l'ID e il segreto di iscrizione dell'identità dell'applicazione e il profilo di connessione della rete, uno sviluppatore di applicazioni può utilizzare gli SDK Fabric o il client CA Fabric per generare i certificati lato client. Puoi utilizzare la seguente procedura per iscrivere un'identità dell'applicazione utilizzando l'[SDK Fabric per Node.js](https://fabric-sdk-node.github.io/){: external}.

1. Salva il profilo di connessione sulla tua macchina locale e rinominalo in `connection.json`.
2. Salva il seguente blocco di codice come `enrollUser.js` nella stessa directory del tuo profilo di connessione:

    ```
    'use strict';

    const FabricCAServices = require('fabric-ca-client');
    const { FileSystemWallet, X509WalletMixin } = require('fabric-network');
    const fs = require('fs');
    const path = require('path');

    const ccpPath = path.resolve(__dirname, 'connection.json');
    const ccpJSON = fs.readFileSync(ccpPath, 'utf8');
    const ccp = JSON.parse(ccpJSON);

    async function main() {
      try {

      // Create a new CA client for interacting with the CA.
      const caURL = ccp.certificateAuthorities['<CA_Name>'].url;
      const ca = new FabricCAServices(caURL);

      // Create a new file system based wallet for managing identities.
      const walletPath = path.join(process.cwd(), 'wallet');
      const wallet = new FileSystemWallet(walletPath);
      console.log(`Wallet path: ${walletPath}`);

      // Check to see if we've already enrolled the admin user.
      const userExists = await wallet.exists('user1');
      if (userExists) {
        console.log('An identity for "user1" already exists in the wallet');
        return;
      }

      // Enroll the admin user, and import the new identity into the wallet.
      const enrollment = await ca.enroll({ enrollmentID: '<app_enroll_id>', enrollmentSecret: '<app_enroll_secret>' });
      const identity = X509WalletMixin.createIdentity('<msp_id>', enrollment.certificate, enrollment.key.toBytes());
      await wallet.import('user1', identity);
      console.log('Successfully enrolled client "user1" and imported it into the wallet');

      } catch (error) {
        console.error(`Failed to enroll "user1": ${error}`);
        process.exit(1);
      }
    }

    main();
    ```
    {:codeblock}

3. Modifica `enrollUser.js` per sostituire i seguenti valori:
  - Sostituisci ``<CA_Name>`` con il nome della CA della tua organizzazione. Puoi trovare il nome della CA nella sezione "organizations" del tuo profilo di connessione sotto "Certificate Authorities". Non utilizzare il "caName" presente nella sezione "Certificate Authorities".
  - Sostituisci ``<app_enroll_id>`` con l'ID di registrazione dell'applicazione fornito dal tuo operatore di rete.
  - Sostituisci ``<app_enroll_secret>`` con il segreto di registrazione dell'applicazione fornito dal tuo operatore di rete.
  - Sostituisci ``<msp_id>`` con l'ID MSP della tua organizzazione. Puoi trovare il tuo ID MSP nella sezione "organizations" del tuo profilo di connessione.
4. Passa a `enrollUser.js` utilizzando un terminale ed esegui `node enrollUser.js`. Se il comando viene eseguito correttamente, dovresti vedere il seguente output:

  ```
  Successfully enrolled client "user1" and imported it into the wallet
  ```
  L'SDK creerà e memorizzerà i tuoi certificati all'interno della directory `wallet/user1/` creata dal comando. Questa directory è il portafoglio del file system utilizzato per inviare le transazioni future.

I portafogli utilizzati dagli SDK Fabric sono diversi da quello nella console {{site.data.keyword.blockchainfull_notm}} Platform. Le identità archiviate nel tuo portafoglio della console non possono essere utilizzate direttamente dall'SDK.
{: note}

## Richiamo di uno smart contract utilizzando l'SDK
{: #ibp-console-app-invoke}

Dopo aver generato il certificato di firma e la chiave privata dell'applicazione e averli memorizzati in un portafoglio, sei pronto per inviare una transazione. Devi conoscere il nome dello smart contract e il nome del canale in cui è stato istanziato. Puoi utilizzare la seguente procedura per richiamare uno smart contract utilizzando l'[SDK Fabric per Node.js](https://fabric-sdk-node.github.io/){: external}.


1. Salva il file qui sotto sulla tua macchina locale come `invoke.js`. Salva il file nella stessa directory di `enrollUser.js`

    ```
    'use strict';

    const { FileSystemWallet, Gateway } = require('fabric-network');
    const fs = require('fs');
    const path = require('path');

    async function main() {
      try {

        // Parse the connection profile. This would be the path to the file downloaded
        // from the IBM Blockchain Platform operational console.
        const ccpPath = path.resolve(__dirname, 'connection.json');
        const ccp = JSON.parse(fs.readFileSync(ccpPath, 'utf8'));

        // Configure a wallet. This wallet must already be primed with an identity that
        // the application can use to interact with the peer node.
        const walletPath = path.resolve(__dirname, 'wallet');
        const wallet = new FileSystemWallet(walletPath);

        // Create a new gateway, and connect to the gateway peer node(s). The identity
        // specified must already exist in the specified wallet.
        const gateway = new Gateway();
        await gateway.connect(ccp, { wallet, identity: 'user1' , discovery: {enabled: true, asLocalhost:false }});

        // Get the network channel that the smart contract is deployed to.
        const network = await gateway.getNetwork('<channel_name>');

        // Get the smart contract from the network channel.
        const contract = network.getContract('<smart_contract_name>');

        // Submit the 'createCar' transaction to the smart contract, and wait for it
        // to be committed to the ledger.
        await contract.submitTransaction('createCar', 'CAR12', 'Honda', 'Accord', 'Black', 'Tom');
        console.log('Transaction has been submitted');

        await gateway.disconnect();

        } catch (error) {
          console.error(`Failed to submit transaction: ${error}`);
          process.exit(1);
        }
      }
    main();
    ```
    {:codeblock}

2. Modifica `invoke.js` per sostituire i seguenti valori:
  - Sostituisci ``<channel_name>`` con il nome del canale in cui è stato istanziato lo smart contract. Puoi trovare il nome della tua CA nella sezione "Certificate Authorities" del tuo profilo di connessione.
  - Sostituisci ``<smart_contract_name>`` con il nome dello smart contract installato. Puoi ottenere questo valore dal tuo operatore di rete.
  - Modifica il contenuto di `submitTransaction` per richiamare una funzione all'interno del tuo smart contract. Il file `invoke.js` viene scritto per richiamare lo [smart contract fabcar](https://github.com/hyperledger/fabric-samples/tree/release-1.4/chaincode/fabcar){: external}. Se vuoi eseguire il file sottostante per inviare una transazione, installa fabcar e istanzia lo smart contract su uno dei tuoi canali.

3. Passa a `invoke.js` utilizzando un terminale ed esegui `node invoke.js`. Se il comando viene eseguito correttamente, dovresti vedere il seguente output:

  ```
  Transaction has been submitted
  ```
  {:codeblock}
  Se passi al tuo canale utilizzando la console, sarai in grado di vedere un altro blocco aggiunto dalla transazione.

## Esecuzione dell'esempio di Commercial Paper
{: #ibp-console-app-commercial-paper}

l'[esercitazione sulla commercial paper](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html){: external} nella documentazione di Hyperledger Fabric guida gli sviluppatori in un caso d'uso in cui più parti comprano, vendono e riscattano la commercial paper. Estende l'[argomento relativo allo sviluppo di applicazioni](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/developing_applications.html){: external} fornendo smart contract e codice applicativo di esempio che ti consente di creare e scambiare asset su un'istanza locale di Fabric.

Puoi anche distribuire il codice di esempio dell'esercitazione sulla commercial paper su una rete {{site.data.keyword.blockchainfull_notm}} Platform. Ciò ti consentirà di iniziare rapidamente a interagire con la tua rete e utilizzare l'esempio per scaricare le dipendenze necessarie. Il codice di esempio include anche degli esempi di come importare i certificati in un [portafoglio (wallet)](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/wallet.html){: external} e utilizzare il tuo profilo di connessione per creare un [gateway Fabric](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/gateway.html){: external}. L'esercitazione può essere utilizzata da due organizzazioni differenti per completare transazioni diverse con un singolo asset. Se hai utilizzato l'[Esercitazione: crea una rete](/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network) per distribuire due organizzazioni peer connesse a un canale, puoi interagire con l'esercitazione utilizzando entrambe le organizzazioni.

Segui i passi riportati di seguito per distribuire l'esempio sulla tua rete. Per ulteriori dettagli sugli smart contract e sulla struttura dell'applicazione, puoi esaminare l'[esercitazione sulla commercial paper](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html){: external}.

### Prerequisiti

Prima di poter distribuire l'esempio di commercial paper, dovrai installare gli strumenti necessari sulla tua macchina locale:
  * [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git){: external}
  * [  Node.js ](https://hyperledger-fabric.readthedocs.io/en/release-1.4/prereqs.html#node-js-runtime-and-npm){: external}

Dovrai anche utilizzare un editor di testo per modificare e salvare i file nell'esempio. Puoi utilizzare molti degli editor di alta qualità disponibili gratuitamente, come ad esempio [Visual Studio Code](https://code.visualstudio.com/){: external}, [Atom](https://atom.io/){: external}, [Sublime text](http://www.sublimetext.com/){: external} o [Brackets](http://brackets.io/){: external}.

### Passo uno: Scarica l'esempio

Scarichi l'esempio di commercial paper clonando il [repository di esempi di Fabric](https://github.com/hyperledger/fabric-samples){: external}:

```
git clone https://github.com/hyperledger/fabric-samples.git
```
{:codeblock}

Dopo che hai scaricato gli esempi di Fabric, esegui questi comandi per assicurarti che stai utilizzando la versione degli esempi compatibile con Fabric v1.4.

```
cd fabric-samples
git checkout v1.4.1
```
{:codeblock}

Puoi trovare l'esempio nella cartella `commercial paper` di `fabric-samples`.

```
cd $HOME/fabric-samples/commercial-paper
```
{:codeblock}

L'esercitazione contiene due organizzazioni di esempio, **magnetocorp** e **digibank**. Ogni organizzazione ha il suo proprio codice dell'applicazione di esempio, memorizzato in due cartelle separate nella directory `organization`.

```
cd organization && ls
digibank	magnetocorp
```
{:codeblock}

Nel corso dell'esercitazione, per prima cosa utilizzerai il codice dell'applicazione magnetocorp per emettere una commercial paper. Potrai quindi utilizzare il codice dell'applicazione digibank per acquistare e riscattare tale commercial paper. Entrambe le directory contengono lo stesso smart contract.

Vai al codice dell'applicazione all'interno della directory magnetocorp.

```
cd magnetocorp/application
```
{:codeblock}

Una volta dentro la directory, puoi scaricare le dipendenze dell'applicazione immettendo il seguente comando:

```
npm install
```
{:codeblock}

### Passo due: Installa e istanzia lo smart contract

Puoi trovare lo smart contract della commercial paper nella cartella `contract` della directory `digibank` e `magnetocorp`. Devi installare questo smart contract su tutti i peer delle organizzazioni utilizzando l'esercitazione. Dovrai quindi istanziare il contratto della commercial paper su un canale. Lo smart contract deve essere impacchettato in [formato .cds](https://hyperledger-fabric.readthedocs.io/en/release-1.4/chaincode4noah.html#packaging){: external} per essere installato utilizzando la console.

Puoi utilizzare l'[estensione {{site.data.keyword.blockchainfull_notm}} VS Code](/docs/services/blockchain?topic=blockchain-develop-vscode) per impacchettare lo smart contract. Dopo aver installato l'estensione, utilizza Visual Studio Code per aprire la cartella `contracts` nel tuo spazio di lavoro. Apri la scheda _{{site.data.keyword.blockchainfull_notm}} Platform_. Nel riquadro _{{site.data.keyword.blockchainfull_notm}} Platform_, vai alla sezione dei pacchetti di smart contract e fai clic su **Package a Smart Contract Project**. L'estensione VS code utilizzerà i file contenuti nella cartella `contracts` per creare un nuovo pacchetto denominato `papernet-js@.0.0.1.cds`. Fai clic con il tasto destro del mouse su questo pacchetto per esportarlo nel tuo file system locale. Puoi quindi usare la tua console per [installare gli smart contract sui tuoi peer](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-install) e in seguito [istanziare lo smart contract su un canale](/docs/services/blockchain/howto?topic=blockchain-ibp-console-smart-contracts#ibp-console-smart-contracts-instantiate).

### Passo tre: Genera i certificati per il tuo portafoglio

Le applicazioni devono firmare le richieste che inviano ai componenti Fabric. Se i componenti non riconoscono le organizzazioni che inviano le transazioni, le transazioni verranno rifiutate e restituiranno un errore. L'esempio di commercial paper crea un portafoglio del file system che memorizzerà i tuoi certificati e firmerà le tue transazioni. Per ulteriori informazioni su come le applicazioni utilizzano i portafogli, vedi l'argomento relativo ai [portafogli](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/wallet.html){: external} nella documentazione di Fabric. I portafogli utilizzati dagli SDK Fabric sono diversi da quello nella console {{site.data.keyword.blockchainfull_notm}} Platform. Le identità archiviate nel tuo portafoglio della console non possono essere utilizzate direttamente dall'SDK.

L'esempio originale utilizza il file `addToWallet.js` per creare un portafoglio del file system utilizzando i certificati dalla cartella degli esempi di Fabric. Creeremo un nuovo file che utilizza l'SDK per generare certificati lato client e memorizzarli direttamente all'interno di un nuovo portafoglio.

Scegli la CA dell'organizzazione che vuoi adoperare per utilizzare l'esercitazione come magnetocorp. Ad esempio, puoi usare Org1 se hai completato l'esercitazione Crea una rete. Utilizza la CA per [creare un'identità dell'applicazione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-identities). **Salva** l'ID e il segreto di registrazione.

Utilizza la tua console per [scaricare il profilo di connessione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-profile). Salva il profilo di connessione sul tuo file system locale e rinominalo in `connection.json`. Utilizza quindi il seguente comando per spostare il profilo di connessione in una directory a cui verrà fatto riferimento da comandi futuri.

  ```
  mv $HOME/<path_to_creds>/connection.json /gateway/connection.json
  ```
  {:codeblock}

Passa alla directory `/magnetocorp/application` e salva il seguente blocco di codice come `enrollUser.js`.

    ```
    'use strict';

    const FabricCAServices = require('fabric-ca-client');
    const { FileSystemWallet, X509WalletMixin } = require('fabric-network');
    const fs = require('fs');
    const path = require('path');

    const ccpPath = path.resolve(__dirname, '../gateway/connection.json');
    const ccpJSON = fs.readFileSync(ccpPath, 'utf8');
    const ccp = JSON.parse(ccpJSON);

    async function main() {
      try {

        // Create a new CA client for interacting with the CA.
        const caURL = ccp.certificateAuthorities['<CA_Name>'].url;
        const ca = new FabricCAServices(caURL);

        // Create a new file system based wallet for managing identities.
        const wallet = new FileSystemWallet('../identity/user/isabella/wallet');

        // Check to see if we've already enrolled the admin user.
        const userExists = await wallet.exists('user1');
        if (userExists) {
          console.log('An identity for "user1" already exists in the wallet');
          return;
        }

        // Enroll the admin user, and import the new identity into the wallet.
        const enrollment = await ca.enroll({ enrollmentID: '<app_enroll_id>', enrollmentSecret: '<app_enroll_secret>' });
        const identity = X509WalletMixin.createIdentity('<msp_id>', enrollment.certificate, enrollment.key.toBytes());
        await wallet.import('user1', identity);
        console.log('Successfully enrolled client "user1" and imported it into the wallet');

        } catch (error) {
          console.error(`Failed to enroll "user1": ${error}`);
          process.exit(1);
        }
    }
    main();
    ```
    {:codeblock}

Prendiamoci un momento per verificare come funziona questo file prima di modificarlo. Innanzitutto, `enrollUser.js` importa le classi `FileSystemWallet` e `X509WalletMixin` dalla libreria `fabric-network`.

```
const FabricCAServices = require('fabric-ca-client');
const { FileSystemWallet, X509WalletMixin } = require('fabric-network');
```
{:codeblock}

Il file utilizza quindi la classe `FileSystemWallet` per creare un portafoglio sul tuo file system locale. Puoi modificare la seguente riga per memorizzare il portafoglio in un'ubicazione diversa.

```
const wallet = new FileSystemWallet('../identity/user/isabella/wallet')
```
{:codeblock}

Dopo aver creato il portafoglio, il frammento di codice utilizza l'ID e il segreto di iscrizione per eseguire l'iscrizione utilizzando la CA della tua organizzazione. Quindi crea un'identità per il certificato di firma e la chiave privata che li importa nel portafoglio. Nota come il file passa anche l'ID MSP della tua organizzazione nel portafoglio.

```
// Enroll the admin user, and import the new identity into the wallet.
const enrollment = await ca.enroll({ enrollmentID: '<app_enroll_id>', enrollmentSecret: '<app_enroll_secret>' });
const identity = X509WalletMixin.createIdentity('<msp_id>', enrollment.certificate, enrollment.key.toBytes());
wallet.import('user1', identity);
console.log('Successfully enrolled client "user1" and imported it into the wallet');
```
{:codeblock}

**Modifica** `enrollUser.js` per sostituire i seguenti valori:
- Sostituisci `'<CA_Name>'` con il nome della CA della tua organizzazione. Puoi trovare il nome della CA nella sezione "organizations" del tuo profilo di connessione sotto "Certificate Authorities". Non utilizzare il "caName" presente nella sezione "Certificate Authorities".
- Sostituisci `'<app_enroll_id>` con l'ID di registrazione dell'applicazione fornito dal tuo operatore di rete.
- Sostituisci `'<app_enroll_secret>'` con il segreto di registrazione dell'applicazione fornito dal tuo operatore di rete.
- Sostituisci `'<msp_id>'` con l'ID MSP della tua organizzazione. Puoi trovare questo ID MSP nella sezione "organizations" del tuo profilo di connessione.

Salva `enrollUser.js` e chiudilo. Nella directory `magnetocorp`, esegui questo comando:
```
node enrollUser.js
```
{:codeblock}

Se il comando termina correttamente, dovresti vedere il seguente output:

```
Successfully enrolled client "user1" and imported it into the wallet
```
{:codeblock}

Puoi trovare il portafoglio che è stato creato nella cartella `identity` della directory `magnetocorp`.

### Passo quattro: Utilizza il profilo di connessione per creare un gateway Fabric

Il [flusso di transazioni](https://hyperledger-fabric.readthedocs.io/en/release-1.4/txflow.html){: external} di Hyperledger Fabric si estende su più componenti, dove le applicazioni client svolgono un ruolo unico. La tua applicazione deve connettersi ai peer che devono approvare la transazione e al servizio di ordine che ordinerà la transazione e la aggiungerà in un blocco. Puoi fornire gli endpoint di questi nodi alla tua applicazione utilizzando il tuo profilo di connessione per costruire un gateway Fabric. Il gateway conduce quindi le interazioni di basso livello con la tua rete Fabric. Per ulteriori informazioni, consulta l'argomento relativo al [gateway Fabric](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/gateway.html){: external} nella documentazione di Fabric.

Hai già scaricato il tuo profilo di connessione e lo hai utilizzato per connetterti all'Autorità di certificazione (CA) della tua organizzazione. Ora useremo il profilo di connessione per creare un gateway.

Apri il file `issue.js` in un editor di testo. Prima di modificare il file, nota che questo importa le classi `FileSystemWallet` e `Gateway` dalla libreria della rete Fabric.

```
const { FileSystemWallet, Gateway } = require('fabric-network')
```
{:codeblock}

La classe `Gateway` è utilizzata per costruire un gateway che userai per inviare la tua transazione.

```
const gateway = new Gateway()
```
{:codeblock}

La classe `FileSystemWallet` è utilizzata per caricare il portafoglio che hai creato nel passo precedente. **Modifica** la seguente riga se hai cambiato l'ubicazione del portafoglio sul tuo file system.

```
const wallet = new FileSystemWallet('../identity/user/isabella/wallet');
```
{:codeblock}

Dopo aver importato il tuo portafoglio, utilizza il seguente codice per passare il tuo profilo di connessione e il portafoglio al nuovo gateway. Dovrai apportare le seguenti **Modifiche** al codice in modo che somigli al frammento di codice riportato di seguito. Le righe che stampano i log sono state rimosse per la brevità.
- Aggiorna `userName` in modo che corrisponda al valore che hai selezionato per `identityLabel` in `enrollUser.js`.
- Aggiorna le opzioni di rilevamento per usufruire del rilevamento dei servizi sulla tua rete. Imposta `discovery: { enabled: true, asLocalhost: false }`.  
- Aggiorna la sezione che importa il tuo profilo di connessione. Il profilo di connessione della console è in formato JSON anziché un file YAML come utilizzato dall'esempio.  

```
const userName = 'user1';

// Load connection profile; will be used to locate a gateway
const ccpPath = path.resolve(__dirname, '../gateway/connection.json');
const ccpJSON = fs.readFileSync(ccpPath, 'utf8');
const connectionProfile = JSON.parse(ccpJSON);

// Set connection options; identity and wallet
let connectionOptions = {
  identity: userName,
  wallet: wallet,
  discovery: { enabled: true, asLocalhost: false }
};

await gateway.connect(connectionProfile, connectionOptions);
```
{:codeblock}

Questo frammento di codice utilizza il gateway per aprire connessioni gRPC ai nodi peer e ordinante e interagire con la tua rete.

### Passo cinque: Richiama lo smart contract

Dopo aver configurato il gateway per la connessione alla rete gestita dalla tua console, modificheremo la parte del file `issue.js` che si connette allo smart contract della commercial paper. Dovrai fornire al gateway il nome del contratto e il canale su cui hai istanziato lo smart contract.

**Modifica** la seguente riga, sostituendo `mychannel` con il tuo nome di canale.

```
const network = await gateway.getNetwork('mychannel');
```
{:codeblock}

Seguendo una riga di codice che stampa un messaggio sulla tua console, puoi trovare una riga che fornisce al gateway il nome dello smart contract. **Modifica** la seguente riga per cambiare il nome `papercontract` con il nome del contratto che hai installato.

```
const contract = await network.getContract('papercontract-js', 'org.papernet.commercialpaper');
```
{:codeblock}

Il gateway ora ha tutte le informazioni che gli servono per inviare una transazione. La seguente riga richiama la funzione `issue` nel contratto della commercial paper, con gli argomenti che definiscono il nuovo asset di commercial paper.

```
const issueResponse = await contract.submitTransaction('issue', 'MagnetoCorp', '00001', '2020-05-31', '2020-11-30', '5000000');
```
{:codeblock}

Dopo aver inviato la transazione utilizzando il gateway, il file `issue.js` disconnette la connessione del gateway.

```
gateway.disconnect();
```
{:codeblock}

Questo comando chiude le connessioni gRPC aperte dal tuo gateway. La chiusura delle connessioni salverà le risorse di rete e migliorerà le prestazioni.

Dopo aver completato le modifiche in questo passo e nel **Passo quattro**, salva il file `issue.js` e chiudilo. Invia la transazione che crea la nuova commercial paper utilizzando il seguente comando:

```
node issue.js
```
{:codeblock}

Se la transazione ha esito positivo, dovresti essere in grado di vedere il seguente output nel tuo terminale:

```
Transaction complete.
Disconnect from Fabric gateway.
Issue program complete.
```

### Passo sei: Utilizza l'esempio come digibank

Dopo aver creato la commercial paper utilizzando magnetocorp, puoi acquistare e riscattare la commercial paper utilizzando l'esercitazione come digibank. Puoi utilizzare il codice dell'applicazione digibank utilizzando la stessa organizzazione di magnetocorp o utilizzare la CA, i peer e il profilo di connessione di un'organizzazione diversa. Se hai completato l'[Esercitazione: crea una rete](/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network), questa è una buona opportunità per utilizzare l'esercitazione come Org2.

Vai alla directory `digibank/application`. Puoi seguire le istruzioni fornite nel **Passo tre** per generare i certificati e il portafoglio che firmeranno la transazione come digibank. Puoi quindi utilizzare il file `buy.js` per acquistare la commercial paper da magnetocorp e utilizzare `redeem.js` per riscattarla. Puoi seguire il **Passo quattro** e il **Passo cinque** per modificare questi file in modo che puntino al profilo di connessione, canale e smart contract appropriati.

## Connessione alla tua rete utilizzando le API SDK Fabric di basso livello
{: #ibp-console-app-low-level}

Se sei interessato a preservare il tuo codice applicazione esistente o a utilizzare gli SDK Fabric per linguaggi diversi da Node.js, puoi ancora connetterti alla tua rete utilizzando API SDK Fabric di livello inferiore. Utilizza la console per [scaricare il tuo profilo di connessione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-profile). Puoi quindi importare gli endpoint dei peer e dei nodi di ordine del tuo canale direttamente dal profilo di connessione o utilizzare le informazioni sull'endpoint dei nodi per aggiungere manualmente gli oggetti peer e ordinante. Dovrai anche utilizzare la tua CA per [creare un'identità dell'applicazione](/docs/services/blockchain/howto?topic=blockchain-ibp-console-app#ibp-console-app-identities) e quindi utilizzare le informazioni sull'endpoint CA per eseguire l'iscrizione sul lato client o generare i certificati utilizzando la console.

La documentazione dell'[SDK Node Fabric](https://fabric-sdk-node.github.io){: external} fornisce un'esercitazione su come [stabilire una connessione alla tua rete utilizzando un profilo di connessione](https://fabric-sdk-node.github.io/tutorial-network-config.html){: external}. L'esercitazione utilizza le informazioni sull'endpoint CA nel tuo profilo di connessione per generare chiavi utilizzando l'SDK. Puoi anche utilizzare la tua console per generare un certificato di firma e una chiave privata e convertire le chiavi in formato PEM. Puoi quindi impostare un contesto utente passando le tue chiavi direttamente alla [classe Client Fabric](https://fabric-sdk-node.github.io/Client.html){: external} degli SDK utilizzando il seguente codice:

```
fabric_client.createUser({
		username: 'admin',
		mspid:  'org1',
		cryptoContent: {
			privateKeyPEM: fs.readFileSync(path.join(__dirname,'./privateKey.pem')),
			signedCertPEM: fs.readFileSync(path.join(__dirname,'./certificate.pem'))
		}});
```
{:codeblock}

Se utilizzi le API SDK di basso livello per connetterti alla tua rete, puoi completare ulteriori passi per gestire le prestazioni e la disponibilità della tua applicazione. Per ulteriori informazioni, vedi [Prassi ottimali per connettività e disponibilità delle applicazioni](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-app-connectivity-availability).


## Utilizzo degli indici con CouchDB
{: #console-app-couchdb}

Se utilizzi CouchDB come tuo database dello stato, puoi eseguire query di dati JSON dai tuoi smart contract rispetto ai dati di stato del canale. Si consiglia vivamente di creare degli indici per le tue query JSON e di usarli nei tuoi smart contract. Gli indici consentono alle tue applicazioni di richiamare i dati in modo efficiente quando la tua rete aggiunge ulteriori blocchi di transazioni e voci nello stato globale. Per informazioni su come utilizzare gli indici con gli smart contract e le applicazioni, vedi [Prassi ottimali quando si utilizza CouchDB](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-app-couchdb-indices).
