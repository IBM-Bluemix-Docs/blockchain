---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-05"

keywords: Starter Plan, Enterprise Plan, peer fee, membership fee

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Prezzi
{: #ibp-pricing}


Questo manuale ti aiuta a comprendere i prezzi per i piani di adesione {{site.data.keyword.blockchainfull}} Platform e quanto pagherai man mano che sviluppi e accresci la tua rete blockchain.  
{:shortdesc}

{{site.data.keyword.blockchainfull_notm}} Platform addebita mensilmente i costi per adesioni e peer alle organizzazioni che creano delle reti blockchain. I costi sono diversi, a seconda del piano di adesione da te scelto e delle risorse di rete utilizzate dalla tua rete. La seguente tabella mostra una panoramica dei prezzi di {{site.data.keyword.blockchainfull_notm}} Platform.

| Elementi dei prezzi | Costo del piano Starter al mese | Costo del piano Enterprise al mese |
|-----|-----|-----|
| Costo adesione | $250 | $1000 |
| Costo peer | $125 | $1000 |

*Figura 1. Panoramica dei prezzi di {{site.data.keyword.blockchainfull_notm}} Platform*

Il costo mensile viene addebitato ogni giorno su base proporzionale. Ad esempio, un membro (costo di adesione associato di $1.000) di due peer (costo per ogni peer di $1.000 X 2 peer) deve pagare $3.000 ogni mese. Se il mese ha 30 giorni, il membro paga $ 100 ($3.000/30) ogni giorno. Per ulteriori informazioni su come pagare per le tue reti, consulta [Modalità di pagamento](/docs/services/blockchain/howto/paying_mode.html#paying-mode).


## Componenti di base della rete
{: #ibp-pricing-components}

Per comprendere i prezzi, dobbiamo iniziare con un'introduzione ai componenti di base di una rete. {{site.data.keyword.blockchainfull_notm}} Platform consente la creazione di una rete blockchain che si basa su Hyperledger Fabric. Ad un alto livello, una rete blockchain Fabric è costituita dai seguenti componenti di base:

-	**Organizzazioni** – Qualsiasi entità che deve mantenere una copia del libro mastro blockchain e deve convalidare le transazioni. Ci possono essere più organizzazioni blockchain per una singola società.
-	**Peer** – Il nodo associato a un'organizzazione che contiene il libro mastro blockchain e convalida le transazioni. I peer sono associati a una singola organizzazione blockchain.
-	**Servizio di ordinazione** – Composto da un singolo ordinante (SOLO) o da una raccolta di ordinanti. Il servizio ordini mette in sequenza le transazioni, crea blocchi e invia questi blocchi ai peer per la convalida.
-	**CA (Certificate Authority, Autorità di certificazione)** – Emette certificati digitali per scopi di identificazione a qualsiasi componente di rete interattivo.

{{site.data.keyword.blockchainfull_notm}} Platform offre due piani di adesione, il **piano Starter** e il **piano Enterprise**, che puoi scegliere in {{site.data.keyword.cloud_notm}}. Entrambi i piani ti consentono di creare organizzazioni e ti forniscono una CA (Certificate Authority, Autorità di certificazione). I piani differiscono per quanto riguarda peer, CA e servizio ordini.

Il piano Enterprise ti fornisce CA e peer altamente disponibili con un servizio ordini con tolleranza agli errori di arresto anomalo. Il piano Starter non ha opzioni di alta disponibilità e utilizza un servizio ordini di base di tipo SOLO. Per tale motivo, il piano Starter è progettato per essere il punto d'ingresso a {{site.data.keyword.blockchainfull_notm}} Platform per ambienti di sviluppo, test e PoC (proof-of-concept). Il piano Enterprise è l'opzione per le reti pronte per gli ambienti pilota e di produzione.

## Elementi chiave dei prezzi
{: #ibp-pricing-key-elements}

Il piano Starter e il piano Enterprise hanno due elementi di prezzo:

- **Costo di adesione** – Copre la creazione dell'organizzazione e l'accesso a servizio ordini e CA e viene addebitato in base alle **singole istanze**. Incluso in questo elemento di prezzi, {{site.data.keyword.blockchainfull_notm}} Platform gestisce il servizio ordini e la CA per conto della tua rete. Questo costo è necessario per avere accesso a una rete creata su {{site.data.keyword.blockchainfull_notm}} Platform.

  -	Il piano Starter ti consente un numero *illimitato* di organizzazioni per ogni singola adesione e la capacità di passare da un'organizzazione all'altra nel monitoraggio della rete. Poiché il piano Starter è progettato per gli ambenti di sviluppo, test e PoC, puoi eseguire una simulazione negli ambienti con più organizzazioni. **Nota** che l'archiviazione di rete totale è limitata a 20 GB, compresi componenti, chaincode e dati del libro mastro. Le tue organizzazioni simulate condividono l'archiviazione di 20-GB nella rete blockchain.

  -	Enterprise consente una singola organizzazione per ogni singola adesione. Poiché Enterprise è progettato per gli ambienti pilota e di produzione, sei collegato alla tua organizzazione specifica.

-	**Costo peer** – Copre i peer di un'organizzazione e viene addebitato in base ai **singoli peer**. Questo costo è obbligatorio solo se desideri avere un peer per mantenere una copia del libro mastro e convalidare le transazioni.

### Esempio di costo di adesione
{: #ibp-pricing-example}

La Figura 2 mostra un esempio di istanze di rete che può aiutare a comprendere il costo di adesione. Nella figura, lo specifico account {{site.data.keyword.cloud_notm}} esegue il provisioning di tre istanze di rete: una istanza di piano Enterprise con il nome *Blockchain-11* e due istanze di piano Starter con i nomi *Blockchain-cz* e *Blockchain-da*. Ogni istanza richiede un servizio ordini e una CA propri. In questo caso, questo specifico account {{site.data.keyword.cloud_notm}} deve pagare tre costi di adesione, uno per ciascuna istanza di rete.

![Istanze di rete blockchain](../images/ibp_instance_example.png "Istanze di rete blockchain")  
*Figura 2. Istanze di rete blockchain*


## Prezzi del piano Starter
{: #ibp-pricing-starter-pricing}

Il provisioning delle reti di piano Starter viene eseguito con una configurazione predefinita di due organizzazioni e un peer per ogni singola organizzazione, per un totale di $500 al mese. Con la configurazione predefinita, non c'è un bisogno immediato di modificare l'ambiente per iniziare a lavorare. Puoi aggiungere ulteriori organizzazioni gratuitamente e puoi aggiungere ulteriori peer alle tue organizzazioni a un costo di $125 al mese per ogni singolo peer. La tua fattura è riflessa nella Figura 3 se crei, o aderisci a, una rete di piano Starter con la configurazione predefinita.

| Componenti dei prezzi | Costo al mese |
|-----|----------------|
| Costo adesione | $250 |
| Costo peer | $125 |
| Costo peer | $125 |
| Addebito a fine mese | $500 |

*Figura 3. Addebito di una rete di piano Starter predefinita*

### Prezzi del piano Starter di esempio
{: #ibp-pricing-starter-plan-pricing-example}

#### Peer aggiuntivi
{: #ibp-pricing-additional-peers}

Il piano Starter non limita il numero di peer che puoi aggiungere alla tua rete. Se aggiungi, ad esempio, due peer alla rete di piano Starter predefinita, uno per ciascuna delle tue organizzazioni, aumenti la tua fattura di $250 al mese. La tua fattura è riflessa nella Figura 4 se aggiungi due peer aggiuntivi all'inizio del primo mese quando crei, o aderisci a, una rete di piano Starter.

| Componenti dei prezzi | Costo al mese |
|-----|----------------|
| Spesa di adesione rete 1 | $250 |
| Costo peer | $125 |
| Costo peer | $125 |
| Costo peer | $125 |
| Costo peer | $125 |
| Totale | $750 |
| Addebito alla fine del primo mese | $750 |

*Figura 4. Addebito di una rete piano Starter predefinita con due peer aggiuntivi*

#### Reti aggiuntive
{: #ibp-pricing-additional-networks}
Anche il piano Starter non limita il numero di istanze di rete di cui puoi eseguire il provisioning. Se esegui il provisioning di una seconda istanza di rete piano Starter, devi pagare una seconda spesa di adesione e una seconda serie di spese peer associate alla seconda rete. Aumenti, pertanto, la tua fattura di $500 al mese per utilizzare la configurazione di rete predefinita. Ti potresti trovare nello scenario in cui hai bisogno di reti Starter aggiuntive per i tuoi ambienti di sviluppo, test e PoC (proof-of-concept) isolati l'uno dall'altro. Un esempio è ad esempio quando desideri consentire ai tuoi ingegneri responsabili della qualità un ambiente di test per eseguire una significativa attività di test funzionale lontana dal tuo ambiente di sviluppo.

La tua fattura è riflessa nella Figura 5 se aggiungi una rete aggiuntiva all'inizio del primo mese quando crei, o aderisci a, una rete di piano Starter.

| Componenti dei prezzi | Costo al mese |
|-----|----------------|
| Spesa di adesione rete 1 | $250 |
| Costo peer | $125 |
| Costo peer | $125 |
| Spesa di adesione rete 2 | $250 |
| Costo peer | $125 |
| Costo peer | $125 |
| Addebito alla fine del primo mese | $1000  |

*Figura 5. Addebito di due reti piano Starter predefinite*

#### Rimozione di peer
{: #ibp-pricing-removing-peers}

Puoi anche rimuovere un peer dalla configurazione di rete piano Starter predefinita. In questa situazione, la tua fattura verrà ridotta di 125 dollari al mese. Ti potresti ritrovare in questo scenario quando stai collaborando con un altro membro nel tuo ambiente di piano Starter, in cui a ognuno di voi serve solo un singolo peer. La tua fattura è riflessa nella Figura 6 se rimuovi un peer dalla tua rete piano Starter.

| Componenti dei prezzi | Costo al mese |
| ----- | ---------------- |
| Spesa di adesione rete 1 | $250 |
| Costo peer | $125 |
| Costo peer | N/D |
| Addebito alla fine del primo mese |  $375 |

*Figura 6. Addebito di una rete piano Starter predefinita dopo la rimozione di un peer*


## Prezzi del piano Enterprise
{: #ibp-pricing-enterprise-plan}

{{site.data.keyword.blockchainfull_notm}} Platform non fornisce una configurazione predefinita per una rete di piano Enterprise. Puoi scegliere la configurazione con la quale ti piacerebbe iniziare. Quando sei pronto a usare il piano Enterprise, dovresti avere una buona comprensione di cosa dovrebbe fare la tua configurazione di rete. Come procedura ottimale per l'alta disponibilità, consigliamo vivamente un minimo di due peer per ogni organizzazione per garantire che per la tua organizzazione non si verifichi un'interruzione di rete.

Se ti trovi in una rete di piano Enterprise con l'altro membro della rete, e ognuno di voi aggiunge due peer per la propria organizzazione, la fattura di ognuno di voi è riflessa nella Figura 7.

| Componenti dei prezzi | Costo al mese |
|-----|----------------|
| Costo adesione | $1000 |
| Costo peer | $1000 |
| Costo peer | $1000 |
| Addebito a fine mese | $3000 |

*Figura 7. Addebito di una rete piano Enterprise di base*

### Prezzi del piano Enterprise di esempio
{: #ibp-pricing-enterprise-plan-pricing}


#### Peer aggiuntivi
{: #ibp-pricing-enterprise-additional-peers}

Continua con l'esempio di cui sopra, se aggiungi altri due peer alla tua organizzazione. La tua fattura aumenta di $2000 al mese. La tua fattura è riflessa nella Figura 8:

| Componenti dei prezzi | Costo al mese |
|-----|----------------|
| Costo adesione | $1000 |
| Costo peer | $1000 |
| Costo peer | $1000 |
| Costo peer | $1000 |
| Costo peer | $1000 |
| Addebito alla fine del primo mese | $5000 |

*Figura 8. Addebito di una rete di piano Enterprise con quattro peer*

Se l'altro membro mantiene la stessa configurazione di rete, la fattura del membro è uguale a prima (che è riflessa nella Figura 7).

#### Reti aggiuntive
{: #ibp-pricing-enterprise-additional-networks}

Anche il piano Enterprise non limita il numero di istanze di rete di cui puoi eseguire il provisioning o a cui puoi aderire. Se crei una seconda rete piano Enterprise con la stessa configurazione di rete di base, ossia una singola organizzazione con due peer, la tua fattura è riflessa nella Figura 11. Ti potresti ritrovare in questo scenario quando hai creato più reti, hai aderito a più reti o ricorre una combinazione di queste due condizioni.

| Componenti dei prezzi | Costo al mese |
|-----|----------------|
| Spesa di adesione rete 1 | $1000 |
| Costo peer | $1000 |
| Costo peer | $1000|
| Spesa di adesione rete 2 | $1000 |
| Costo peer | $1000 |
| Costo peer | $1000|
| Totale | $6000 |

*Figura 9. Addebito di due reti di piano Enterprise che hanno entrambe la configurazione di rete di base*

Se l'altro membro utilizza solo una rete piano Enterprise e mantiene la stessa configurazione di rete, la fattura del membro è uguale a prima (che è riflessa nella Figura 7).
