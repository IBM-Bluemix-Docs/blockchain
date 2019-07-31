---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Swagger APIs, create a network, join a network, authentication credential

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:gif: data-image-type='gif'}

# Creazione o unione di una rete con le API Swagger
{: #swagger-network}

{{site.data.keyword.blockchainfull}} Platform presenta diverse API REST che puoi utilizzare per creare o unire una rete blockchain in {{site.data.keyword.cloud_notm}}. Puoi provare queste API utilizzando la [IU Swagger](/docs/services/blockchain/howto?topic=blockchain-ibp-swagger#ibp-swagger) associata alla tua rete.
{:shortdesc}


## Richiamo delle credenziali di autenticazione di base della API
{: #swagger-network-retrieve-id-token}

Prima di iniziare, devi creare una [istanza del servizio {{site.data.keyword.blockchainfull_notm}} Platform](https://cloud.ibm.com/catalog/services/ibm-blockchain-5-prod){: external} con il piano Starter o il piano Enterprise in {{site.data.keyword.cloud_notm}}.

Per utilizzare le API Swagger per creare o unire una rete, hai bisogno delle credenziali di autenticazione di base per assicurarti di avere l'accesso all'istanza del servizio in {{site.data.keyword.cloud_notm}}.

1. Nel tuo [dashboard {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/resources){: external}, apri l'istanza del servizio che hai creato.
2. Fai clic su **Credenziali del servizio** dal navigator di sinistra.
3. Fai clic sul pulsante "Nuova credenziale" nella pagina **Credenziali del servizio** per creare una nuova credenziale.
    1. Fornisci un nome alla credenziale, ad esempio *CreateJoin*.
    2. Immetti **{"type": "service_instance_token"}** nel campo "Aggiungi parametro di configurazione inline".
    3. Fai clic sul pulsante **Aggiungi**.
    ![Richiama credenziali del servizio](../images/service_credentials.gif "Richiama credenziali del servizio"){: gif}
4. Dopo avere creato la nuova credenziale, fai clic su **Visualizza credenziali** nell'intestazione **AZIONI** di tale credenziale. I contenuti della credenziale sono simili al seguente esempio:

    ```
    {
      "service_instance_id": "60cc757d-1234-7866-9893-491cec2d0eaa",
      "service_instance_token": "T8-W0rHv_vEya63P8KcVUwxAXXbDmihGcDRD5AcHVXGn6S2jbxx2LikPz8w26c3k",
      "description": "This token can be used with the IBP APIs to create or join a network. It can only be used once."
    }
    ```

    `service_instance_id` viene utilizzato come ID utente di autenticazione di base e `service_instance_token` come password di autenticazione di base. Utilizza questi valori come credenziali di autenticazione di base quando richiami le API **Crea rete** o **Unisciti alla rete**.

    Se crei una rete blockchain prima di seguire i precedenti passi per creare una credenziale del servizio, i contenuti della credenziale includono anche le informazioni sulla rete e sono simili al seguente esempio:

    ```
    {
      "org1": {
        "url": "https://ibp-sp.us-south.ibm-blockchain-5-prod.cloud.ibm.com",
        "network_id": "n5edf19260c998940c5933daca2be76974a",
        "key": "org1",
        "secret": "A8YeuUuNvKVbN5cVGOlwprpaaHCVxYiP0uEN0fviQB2W9_ldJLtMSOSHqkUpkqysMA"
        }
    }    
    ```

    **Nota**: per la API **Invita**, `key` viene utilizzato come ID utente di autenticazione di base e `secret` come password.


## Controllo delle ubicazioni della rete disponibili
{: #swagger-network-check-location}

Puoi utilizzare le API per creare le reti blockchain solo nelle ubicazioni della rete disponibili. Prima di creare una rete, usa la seguente API per ottenere un elenco corrente delle ubicazioni di rete disponibili. Non sono richieste delle credenziali per eseguire questa API:

```
https://ibp-ep.us-south.ibm-blockchain-5-prod.cloud.ibm.com/api/v1/network-locations/available
```
{:codeblock}

Viene restituito un elenco delle ubicazioni di rete disponibili simile al seguente esempio:

```
{
  "DAL": {
    "location_id": "DAL",
    "description": "Dallas",
    "status": "available"
    "swagger_url": "https://ibmblockchain-v2-dal.4.secure.blockchain.ibm.com/api-docs"
  },
  "FFT": {
    "location_id": "FFT",
    "description": "Frankfurt",
    "status": "available"
    "swagger_url": "https://ibmblockchain-v2-fft.2.secure.blockchain.ibm.com/api-docs"
  },
  "TOR": {
    "location_id": "TOR",
    "description": "Toronto",
    "status": "available"
    "swagger_url": "https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api-docs"
  }
}
```

Se intendi creare una rete, seleziona l'ubicazione dove vuoi crearla dall'elenco restituito dalla API. Nota: ``location_id`` e ``swagger_url`` sono associati a tale ubicazione.

Se intendi aderire a una rete, annota lo ``swagger_url`` associato al ``location_id`` specificato nella tua email di invito.

Lo ``swagger_url`` rappresenta l'endpoint api che utilizzerai quando crei una rete, o aderisci a essa, utilizzando le API di seguito indicate.


## Creazione di una rete

**Nota**: se utilizzi piano Starter, non hai bisogno di creare una rete con le API perché viene fornita una rete predefinita quando crei l'istanza del servizio blockchain in {{site.data.keyword.cloud_notm}}.

Se utilizzi piano Enterprise, devi completare due passi per creare una rete con le API.

1. Crea un'istanza del servizio blockchain in {{site.data.keyword.cloud_notm}} con piano Enterprise<!-- or Enterprise Plus Plan-->.  Richiama i tuoi token e ID istanza del servizio come password e nome utente di autenticazione di base. Per ulteriori informazioni, vedi [Richiamo delle credenziali di autenticazione di base della API](/docs/services/blockchain/howto?topic=blockchain-swagger-network#swagger-network-retrieve-id-token).

2. Richiama la API **Crea rete** utilizzando queste credenziali del servizio. Immetti questa API sullo ``swagger_url`` api richiamato da [Controllo delle ubicazioni della rete disponibili](/docs/services/blockchain/howto?topic=blockchain-swagger-network#swagger-network-check-location). Vai allo ``swagger_url link`` per utilizzare l'IU Swagger per immettere la API di creazione della rete oppure immetti a livello programmatico il comando utilizzando l'indirizzo URL senza ``/api-docs``. Ad esempio,

    ```
    https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api/v1/networks
    ```
    {:codeblock}

**Parametri**:
- `location_id`: l'ID di un'ubicazione della rete disponibile. Specifica il valore del `location_id` annotato da [Controllo delle ubicazioni della rete disponibili](/docs/services/blockchain/howto?topic=blockchain-swagger-network#swagger-network-check-location).
- `company_name`: il tuo identificativo come membro della rete.
- `email`: il tuo indirizzo email per ricevere le notifiche.
- `peers`: il numero di peer che vuoi creare per questo membro. I valori validi sono 0 - 6. Puoi inoltre creare i peer per il tuo membro successivamente nella IU Monitoraggio della rete.
- `ledger_type`: il tipo di libro mastro di questa rete. I valori validi sono levelDB e couchDB. **levelDB** è il valore predefinito.


## Invito di nuovi membri in una rete.

Dopo aver creato una rete blockchain, puoi invitare altri membri ad unirsi alla tua rete. Devi specificare l'ID della rete a cui vuoi invitare i nuovi membri ad unirsi. Le credenziali di autenticazione di base necessarie per invitare un membro sono diverse da quelle utilizzate nella API **Crea rete** API. <!--In order to get the basic auth information, you need to follow the same steps in "Retrieving basic auth information for API". --> Puoi ottenere le credenziali per invitare un membro con la API **Richiama credenziali rete** nella [IU Swagger ](/docs/services/blockchain/howto?topic=blockchain-ibp-swagger#ibp-swagger-retrieving-network-credentials) o [richiamare le informazioni di autenticazione di base per la API](/docs/services/blockchain/howto?topic=blockchain-swagger-network#swagger-network-retrieve-id-token) dalla tua istanza del servizio in {{site.data.keyword.cloud_notm}}.

```
/networks/{networkID}/invite
```
{:codeblock}

**Parametri**:
- `email`: l'indirizzo email del membro da invitare nella rete.
- `company_name`: l'identificativo che definisci per il membro per unirsi alla rete. I membri invitati possono modificare i propri identificativi quando si uniscono alla rete.

Il membro invitato riceverà un invito email con le istruzioni su come unirsi alla tua rete.


## Adesione a una rete

Se vieni invitato ad aderire a una rete blockchain, riceverai un'email di invito alla rete che include `location_id` e `network id`.

1. Prima di aderire a una rete devi creare un'istanza del servizio {{site.data.keyword.blockchainfull_notm}} Platform e richiamare i tuoi token e ID istanza del servizio come password e nome utente di autenticazione di base. Per ulteriori informazioni, vedi [Richiamo delle informazioni di autenticazione di base per la API](/docs/services/blockchain/howto?topic=blockchain-swagger-network#swagger-network-retrieve-id-token).

2. [Controlla le ubicazioni di rete disponibili](/docs/services/blockchain/howto?topic=blockchain-swagger-network#swagger-network-check-location) per ottenere lo `swagger_url` per il `location_id` nella tua email di invito. Sarà qualcosa di simile a:

    ```
    https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api-docs
    ```
    {:codeblock}

3. Passa al tuo ``swagger_url`` per utilizzare l'IU Swagger per immettere la API di adesione oppure inoltra a livello programmatico la richiesta di adesione utilizzando lo ``swagger_url``. Sostituisci ``/api-docs`` con ``/api/v1/networks/[network_id]]/join``
e compila il `network_id` utilizzando il valore dalla tua email di invito. L'URL risultante sarà simile al seguente:

    ```
    https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api/v1/networks/56102acee0e4487889ef09db681bada0/join
    ```
    {:codeblock}

    **Nota**: per la API **Unisciti**, utilizza l'ID istanza del servizio e il token che hai richiamato al passo 1 come nome utente e password di autenticazione di base.

**Parametri**:
- `company_name`: il tuo identificativo come membro della rete. Questo sostituirà il nome assegnato dal mittente dell'invito.
- `email`: il tuo indirizzo email per ricevere le notifiche.  Questo dovrebbe corrispondere all'indirizzo email nella notifica di invito.
- `peers`: il numero di peer che vuoi creare per questo membro. I valori validi sono da 0 a 6. Puoi inoltre creare i peer per il tuo membro successivamente nel Monitoraggio della rete.
