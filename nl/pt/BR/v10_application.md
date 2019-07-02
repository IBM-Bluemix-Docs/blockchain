---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Fabric SDKs, client application, enroll, register, chaincode

subcollection: blockchain

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}
{:external: target="_blank" .external}

# Desenvolvendo aplicativos com os SDKs do Fabric
{: #dev-app}

O {{site.data.keyword.blockchainfull}} Platform fornece APIs que podem ser usadas para conectar aplicativos à rede de blockchain. É possível usar os terminais de API da rede no perfil de conexão para chamar seu chaincode e atualizar ou consultar o livro-razão específico do canal em seus peers. Também é possível usar APIs na [IU do Swagger](/docs/services/blockchain/howto?topic=blockchain-ibp-swagger#ibp-swagger) para gerenciar nós, canais e membros de sua rede.
{:shortdesc}

É possível usar este tutorial para aprender como acessar as APIs do {{site.data.keyword.blockchainfull_notm}} Platform e usá-las para inscrever-se e registrar seu aplicativo com a rede. Você também aprenderá como interagir com sua rede e emitir transações por meio de seu aplicativo. O tutorial é baseado no tutorial [Escrevendo seu primeiro aplicativo](https://hyperledger-fabric.readthedocs.io/en/release-1.2/write_first_app.html){: external} na Documentação do Hyperledger Fabric. Você usará muitos dos mesmos arquivos e comandos do tutorial **Escrevendo seu primeiro aplicativo**, mas os utilizará para interagir com uma rede no {{site.data.keyword.blockchainfull_notm}} Platform. Este tutorial descreve cada etapa do desenvolvimento do aplicativo usando o Hyperledger Fabric Node SDK. Você também aprenderá como inscrever-se e registrar usuários usando o cliente Fabric CA como uma alternativa ao uso do SDK.

Além deste tutorial, é possível usar aplicativos de amostra e o chaincode que o {{site.data.keyword.blockchainfull_notm}} Platform fornece como modelos quando você cria suas próprias soluções de negócios. Para obter mais informações, veja [Implementando aplicativos de amostra](/docs/services/blockchain/howto?topic=blockchain-deploying-sample-applications#deploying-sample-applications).

Quando estiver pronto para escalar seu aplicativo, visite as [Melhores práticas para desenvolvimento de aplicativo](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-app).

## Pré-requisitos
{: #dev-app-prerequisites}

São necessários os pré-requisitos a seguir antes de poder usar o tutorial **Gravando o seu primeiro aplicativo** no {{site.data.keyword.blockchainfull_notm}} Platform.

- Se você não tiver uma rede de blockchain no {{site.data.keyword.cloud_notm}}, será necessário criar uma com um Starter ou Enterprise Membership Plan. Para obter mais informações, consulte [Criando uma rede do Starter Plan](/docs/services/blockchain?topic=blockchain-getting-started-with-starter-plan#getting-started-with-starter-plan-creating-a-network) ou [Criando uma rede do Enterprise Plan](/docs/services/blockchain?topic=blockchain-getting-started-with-enterprise-plan).

  Depois de entrar no Monitor de rede de sua rede, inclua pelo menos um peer para sua organização na tela "Visão geral". Em seguida, crie pelo menos um canal em sua rede. Para obter mais informações, consulte [Criando um canal](/docs/services/blockchain/howto?topic=blockchain-ibp-create-channel#ibp-create-channel-creating-a-channel). **Observe** que se você usar uma rede do Starter Plan, sua rede já terá um canal com o nome de `defaultchannel` que poderá ser usado para implementar o chaincode.

- Instale as ferramentas necessárias para fazer download de amostras do Hyperledger Fabric e para usar o Node SDK.
  * [Curl](https://hyperledger-fabric.readthedocs.io/en/release-1.2/prereqs.html#install-curl){: external} ou [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git){: external}
  * [ Node.js ](https://hyperledger-fabric.readthedocs.io/en/release-1.2/prereqs.html#node-js-runtime-and-npm){: external}

- Instale as amostras do Hyperledger Fabric fazendo download do diretório `fabric-samples`. É possível seguir o [guia de introdução](https://hyperledger-fabric.readthedocs.io/en/release-1.2/install.html){: external} na Documentação do Hyperledger Fabric.

- Navegue para o diretório `fabric-samples` em sua máquina local.
  * Use o comando `git checkout` para usar a ramificação que corresponde à versão do Hyperledger Fabric de suas redes. É possível localizar a versão do Fabric abrindo a [janela Preferências de rede](/docs/services/blockchain?topic=blockchain-ibp-dashboard#ibp-dashboard-network-preferences) em seu Network Monitor.
    - Se sua rede estiver no Fabric versão 1.2, será possível usar a ramificação principal.
    - Se sua rede estiver no Fabric versão 1.1, execute `git checkout v1.1.0`.
    - Se sua rede estiver no Fabric versão 1.0, execute `git checkout v1.0.6`.

  * Navegue para `fabric-samples/fabcar`. É possível fazer uma cópia desse diretório e renomeá-la para que seja possível tentar e testar o aplicativo de amostra em um diretório limpo.

  * No diretório `fabcar`, execute o comando `npm install` para instalar os pacotes necessários para usar o Fabric SDK, que incluem `fabric-client` e `fabric-ca-client`.

- Instale e instancie o chaincode do fabcar em seu canal usando o [Monitor de Rede](/docs/services/blockchain/howto?topic=blockchain-install-instantiate-chaincode#install-instantiate-chaincode-install-cc). É possível localizar o chaincode fabcar na pasta `fabric-samples` em `fabric-samples > chaincode > fabcar > go`.

- Recupere o Perfil de conexão de sua rede na tela "Visão geral" do Monitor de rede. Salve o Perfil de conexão em seu diretório `fabcar` e renomeie-o para `creds.json`.

## Usando os SDKs do Fabric
{: #dev-app-fabric-sdks}

Os Hyperledger Fabric SDKs fornecem um conjunto poderoso de APIs que permitem que os aplicativos interajam com redes de blockchain. É possível localizar a lista mais recente de idiomas suportados na [documentação da comunidade do Hyperledger Fabric SDK](https://hyperledger-fabric.readthedocs.io/en/release-1.2/getting_started.html#hyperledger-fabric-sdks){: external}. Recomenda-se usar o Node SDK ou o Java SDK com o {{site.data.keyword.blockchainfull_notm}} Platform. É possível saber mais sobre as APIs fornecidas pelos SDKs nos repositórios individuais dos SDKs.

Este tutorial usa o [Node SDK](https://fabric-sdk-node.github.io/){: external} para registrar e inscrever seu aplicativo e, em seguida, usar o aplicativo para emitir transações chamando e consultando o chaincode. Este tutorial descreve as informações que você precisa fornecer para o SDK para que seu aplicativo possa se conectar à rede de blockchain. Ele também apresenta algumas das APIs que podem ser usadas e como o SDK interage e envia transações para a sua rede de blockchain.

## Incluindo terminais de API de rede em seu aplicativo
{: #dev-app-api-endpoints}

É necessário fornecer ao aplicativo os terminais de API de recursos de rede específicos, incluindo os nós do solicitador, da CA e do peer, na rede de blockchain no {{site.data.keyword.cloud_notm}}. O seu aplicativo pode interagir com a rede por meio desses terminais de API. É possível localizar os terminais de API no Perfil de conexão de sua rede. O Perfil de conexão está no formato JSON e contém as informações sobre terminais de API e os IDs/segredos de inscrição para seus recursos de rede.

1. Recupere as informações do terminal de API de seus recursos de rede por meio de seu Monitor de rede com um dos métodos a seguir:
  * Na tela "Visão geral", clique em **Perfil de conexão**. O Perfil de conexão contém um conjunto completo de informações sobre terminais de API de todos os recursos de rede.
![Perfil de conexão no Monitor de rede](images/service_credentials.png "Perfil de conexão no Monitor de rede")

  * Se você tiver o chaincode em execução na rede, será possível obter as informações sobre terminais de API específicas para o chaincode. Na tela "Canais", clique na linha do canal na qual o chaincode está em execução para abrir a tela do canal específico. Em seguida, localize o chaincode e clique no botão **JSON**.
    ![Terminais de API por chaincode](images/channel_chaincode.png "Terminais de API por chaincode")

2. Localize as informações sobre terminais de API de seus recursos de rede, que são semelhantes à URL da linha `peer1-org1` no exemplo a seguir:
  ```
    "peers": {
        "org1-peer1": {
            "url": "grpcs://n7413e3b503174a58b112d30f3af55016-org1-peer1.us3.blockchain.ibm.com:31002",
            "eventUrl": "grpcs://n7413e3b503174a58b112d30f3af55016-org1-peer1.us3.blockchain.ibm.com:31003",
                  ...
  ```

Você pode desejar destinar recursos de rede fora de sua organização com seu aplicativo. Por exemplo, se uma [política de endosso](/docs/services/blockchain/howto?topic=blockchain-install-instantiate-chaincode#install-instantiate-chaincode-endorsement-policy) de chaincode requerer endossos de outras organizações no canal, será necessário enviar a transação para peers suficientes dessa organização para obedecer à política. A [descoberta de serviço](https://hyperledger-fabric.readthedocs.io/en/release-1.2/discovery-overview.html){: external} no Hyperledger Fabric não é suportada para o plano Starter ou o plano Enterprise. Será necessário obter as informações sobre terminais de peers e os certificados TLS associados de outras organizações usando a seção "peers" de seu Perfil de conexão. É possível entrar em contato com os administradores das outras organizações sobre quais peers eles associaram a canais específicos.{:note}

3. Vincule as informações do terminal de API a um arquivo de configuração de seu aplicativo, conforme mostrado no exemplo a seguir:
  ```
  grpcs://n7413e3b503174a58b112d30f3af55016-orderer.us3.blockchain.ibm.com:31001
  ```

  Também é possível enviar [solicitações de HEAD](/docs/services/blockchain/howto?topic=blockchain-monitor-blockchain-network#monitor-blockchain-network-monitor-nodes) para esses terminais para verificar a disponibilidade de seus recursos de rede.

  Se você estiver usando os SDKs do Fabric, também poderá se conectar à rede usando seu Perfil de conexão. Este tutorial fornece as informações sobre terminais de sua rede para o SDK manualmente. No entanto, é possível localizar um tutorial e orientação sobre [como usar seu perfil de conexão com o SDK](#dev-app-connection-profile) em uma seção posterior.

## Inrolando seu aplicativo
{: #dev-app-enroll}

Antes de conectar um aplicativo à sua rede no {{site.data.keyword.blockchainfull_notm}} Platform, é necessário provar a autenticidade de seu aplicativo para a rede. Não vamos nos aprofundar nos detalhes de certificados x509 e infra-estrutura de chave pública, embora você possa aprender mais visitando o tutorial [Gerenciando certificados no {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates). Simplesmente falando, os fluxos de comunicação no Fabric usam as operações de assinatura/verificação em cada ponto de contato. Portanto, qualquer aplicativo que envie chamadas, como consultas ou atualizações do livro-razão, para a rede, precisa assinar cargas úteis com sua chave privada e anexar um certificado x509 devidamente assinado para propósitos de verificação. **Inscrição** é o processo de geração de chaves e certificados necessários da Autoridade de certificação apropriada. Após a inscrição, seu aplicativo está pronto para se comunicar com a rede.

Essa seção explica como recuperar as chaves e os certificados com o Fabric Node SDK usando o código de amostra que faz parte do tutorial **Escrevendo seu primeiro aplicativo**. É possível gerar certificados apenas usando uma identidade que tenha sido registrada com sua Autoridade de Certificação. O tutorial abaixo primeiro inscreve usando uma identidade de administrador que já foi registrada com sua CA. Em seguida, ele usa esses certificados para registrar uma nova identidade do cliente. O tutorial inscreve novamente usando a nova identidade e usa esses certificados para enviar transações para a rede. <!---You can find an illustration of how the developing applications tutorial interacts with your organization CA in the diagram below.--->

Também é possível usar a tela "Autoridade de certificação" do Monitor de Rede para gerar certificados e usar esses certificados para interagir com a rede. Para saber como, visite [Gerando certificados usando o Monitor de Rede](#dev-app-enroll-panel). Também é possível saber como usar o [cliente Fabric CA](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates-enroll-register-caclient) a partir da linha de comandos para gerar certificados e registrar usuários no tutorial [Gerenciando certificados](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates).

### Inscrição utilizando o Fabric SDK
{: #dev-app-enroll-sdk}

No diretório `fabcar` na pasta `fabric-samples`, abra o arquivo `enrollAdmin.js` em um editor de texto.

1. O arquivo cria primeiro uma instância do cliente Fabric.
  ```
  var fabric_client = new Fabric_Client();
  ```
  {:codeblock}

2. Em seguida, o arquivo cria um armazenamento de valor da chave (KVS) para gerenciar seus certificados. O SDK usa a classe [KeyValueStore](https://fabric-sdk-node.github.io/module-api.KeyValueStore.html){: external} para criar o armazenamento de chave/valor e a classe [CryptoSuite](https://fabric-sdk-node.github.io/module-api.CryptoSuite.html){: external} para executar os cálculos criptográficos. É possível ver o bloco de código relevante abaixo.
  ```
  # create the key value store as defined in the fabric-client/config/default.json 'key-value-store' setting
  Fabric_Client.newDefaultKeyValueStore({ path: store_path
    }).then((state_store) => {
   // assign the store to the fabric client
   fabric_client.setStateStore(state_store);
   var crypto_suite = Fabric_Client.newCryptoSuite();
   // use the same location for the state store (where the users' certificate are kept)
   // and the crypto store (where the users' keys are kept)
   var crypto_store = Fabric_Client.newCryptoKeyStore({path: store_path});
   crypto_suite.setCryptoKeyStore(crypto_store);
   fabric_client.setCryptoSuite(crypto_suite);
   var	tlsOptions = {
     trustedRoots: [],
     verify: false
   };
  ```
  {:codeblock}

3. Após a definição do KVS, é possível usar alguns métodos por meio da classe [Fabric Client](https://fabric-sdk-node.github.io/Client.html){: external} e da API do Fabric-CA-Client <!---[FabricCAServices](https://fabric-sdk-node.github.io/FabricCAServices.html){: external} ---> para se comunicar com o servidor de CA. É necessário fornecer ao SDK o nome e a URL de sua Autoridade de Certificação. Abra o arquivo JSON do **Perfil de conexão** na tela **Visão geral** no Monitor de rede e localize as seguintes variáveis na seção `certificateAuthorites`:
  * URL para CA: `url` sob `certificateAuthorities`
  * ID do usuário administrador: ``enrollId``
  * Senha do administrador: ``enrollSecret``
  * Nome da CA: `caName`

  **Edite** as linhas relevantes no arquivo `enrollAdmin.js` com estas informações da seguinte maneira:
  ```
  fabric_ca_client = new Fabric_CA_Client('https://<enrollID>:<enrollSecret>@<ca_url_with_port>', null ,<caName>, crypto_suite);
  ```
  {:codeblock}

  Por exemplo:
  ```
  fabric_ca_client = new Fabric_CA_Client('https://admin:dda0c53f7b@n7413e3b503174a58b112d30f3af55016-org1-ca.us3.blockchain.ibm.com:31011', null ,'org1CA', crypto_suite);
  ```

  O cliente Fabric, então, verifica se seu aplicativo já está inscrito. **Edite** a linha abaixo com o `enrollID` de seu perfil de conexão:
  ```
  return fabric_client.getUserContext('<enrollID>', true);
  ```
  {:codeblock}

4. É necessário enviar a chamada "inscrever" para o Servidor da CA. Seu `admin` já está registrado com sua rede. A chamada de inscrição recupera uma chave privada e uma chave pública agrupada em um certificado x509 e assinada pela CA de destino. Esse certificado agrupado e assinado é chamado de signCert. O signCert permite que os membros da rede verifiquem chamadas que se originam no cliente. É necessário fornecer seu nome de organização, sua senha e o ID do MSP por meio do arquivo de credenciais. Na seção `certificateAuthorities` de suas credenciais de rede, localize seu `enrollID`, seu `enrollSecret` e seu `x-mspid`. **Edite** o bloco de código abaixo com esses valores e substitua a seção relevante de seu arquivo.
  ```
  return fabric_ca_client.enroll({
    enrollmentID: '<enrollID>',
    enrollmentSecret: '<enrollSecret>'
      }).then((enrollment) => {
    console.log('Successfully enrolled admin user');
    return fabric_client.createUser(
         username: 'admin',
            mspid: '<x-mspid>',
            cryptoContent: { privateKeyPEM: enrollment.key.toBytes(), signedCertPEM: enrollment.certificate }
        });
  ```
  {:codeblock}

5. Salve o arquivo  ` enrollAdmin.js ` .

No diretório `fabcar`, inscreva o administrador emitindo o comando a seguir:
```
enrollAdmin.js do nó
```
{:codeblock}

O comando de inscrição gera o signCert e exporta-o para uma pasta denominada `hfc-key-store`. Os arquivos futuros neste tutorial procurarão seus certificados nesta pasta. Caso possa localizar os certificados de administrador na pasta `hfc-key-store`, o comando enroll funciona.

Se quiser [operar sua rede usando o SDK](#dev-app-operate-sdk), será necessário fazer upload de seu signCert de administrador para o {{site.data.keyword.blockchainfull_notm}} Platform. É possível localizar seu signCert de administrador na pasta `hfc-key-store`. Abra o arquivo `admin` e copie o certificado dentro das aspas após o campo `certificate`. Use uma ferramenta ou um editor de texto para converter o certificado no formato PEM. É possível, então, fazer upload do certificado administrativo para sua rede de blockchain do Monitor de Rede. Para obter mais informações sobre como incluir certificados, veja [a guia "Certificados" da tela "Membro"](/docs/services/blockchain?topic=blockchain-ibp-dashboard#ibp-dashboard-members) no Monitor de rede. Isso não será necessário se você estiver usando apenas o SDK para chamar ou consultar o chaincode.

## Registrando seu aplicativo
{: #dev-app-register}

Depois de gerar os certificados do lado do cliente, é necessário registrar seu aplicativo com a Autoridade de Certificação de rede. O registro inclui seu aplicativo na lista de componentes que a rede pode reconhecer. Uma boa prática é registrar o aplicativo como uma identidade separada, em vez de usar o `admin` para assinar solicitações.

### Registrando usando o SDK
{: #dev-app-register-sdk}

É possível usar o arquivo `registerUser.js` para registrar e inscrever o aplicativo como `user1` usando seu signCert `admin`. Abra  ` registerUser.js `  em um editor de texto.

1. Forneça a URL e o nome da CA para uma nova instância do cliente Fabric CA.

2. Forneça o enrollID para o método `getUserContext` da [classe Fabric Client](https://fabric-sdk-node.github.io/Client.html){: external} para verificar se seu `admin` está inscrito e tem permissão para emitir essa solicitação. **Edite** o bloco de códigos relevante em seu arquivo com base na amostra abaixo:
  ```
  // be sure to change the http to https when the CA is running TLS enabled
  fabric_ca_client = new Fabric_CA_Client('https://admin:dda0c53f7b@n7413e3b503174a58b112d30f3af55016-org1-ca.us3.blockchain.ibm.com:31011', null , '<caName>', crypto_suite);

  // first check to see if the admin is already enrolled
  return fabric_client.getUserContext('admin', true);
  }).then ((user_from_store) = > {
  if (user_from_store & & user_from_store.isEnrollroll()) {
      console.log('Successfully loaded admin from persistence');
      admin_user = user_from_store;
  } else {
      throw new Error (' Falha ao obter admin .... executar enrollAdmin.js '); }
  ```
  {:codeblock}

3. Use o **Cliente de CA do Fabric** para registrar e inscrever o usuário com a CA e, em seguida, use o **Cliente do Fabric** para criar o novo signCert. **Edite** o bloco a seguir com seu ID do MSP e sua afiliação da organização. É possível localizar suas `x-affiliations` na seção de autoridades de certificação de suas credenciais de rede e usar qualquer afiliação listada. Inclua o nome do usuário que você deseja criar. A amostra fabcar usa `user1` por padrão.
  ```
  return fabric_ca_client.register({enrollmentID: 'user1', affiliation: '<x-affiliations>',role: 'client'}, admin_user)
    ...
  return fabric_ca_client.enroll({enrollmentID: 'user1', enrollmentSecret: secret});
  }).then ((cadastramento) = > {
  console.log('Successfully enrolled member user "user1" ');
  return fabric_client.createUser(
   {username: 'user1',
   mspid: '<x-mspid>',
   cryptoContent: { privateKeyPEM: enrollment.key.toBytes(), signedCertPEM: enrollment.certificate }
   });
  ```
  {:codeblock}

4. Salve o arquivo  ` registerUser.js ` .

Execute o comando `node registerUser.js` para registrar e inscrever o `user1`. Caso possa localizar os certificados de `user1` na pasta `hfc-key-store`, o comando funciona. É possível registrar somente uma identidade a cada vez. Se você tiver problemas, tente executar `registerUser.js` com um novo nome de usuário.

### Registrando-se utilizando o Monitor de Rede

Como alternativa, é possível registrar e inscrever seu aplicativo cliente usando a guia **Autoridade de certificação** do Monitor de rede. Consulte estas [informações](/docs/services/blockchain?topic=blockchain-ibp-dashboard#ibp-dashboard-ca) para obter mais instruções.

## Emitindo transações chamando e consultando o chaincode
{: #dev-app-invoke-query}

Seu aplicativo precisa interagir com a rede de blockchain completa para enviar uma transação.

1. O aplicativo envia uma proposta de transação para ser endossada por peers no canal.
2. Os peers endossadores retornam a transação endossada para o aplicativo.
3. O aplicativo envia a transação endossada para o serviço de ordenação incluir a transação no livro-razão.

Para obter mais informações sobre o fluxo de transação completo, consulte [Fluxo de transação](https://hyperledger-fabric.readthedocs.io/en/release-1.2/txflow.html){: external} na Documentação do Hyperledger Fabric. Depois de iniciar com este tutorial, visite a seção de [conectividade e disponibilidade do aplicativo](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-app-connectivity-availability) para obter dicas sobre como gerenciar a interação do SDK com a rede.

As amostras a seguir demonstram como o Node SDK configura a topologia de rede, define a proposta de transação e, em seguida, envia a transação para a rede. É possível usar o arquivo `invoke.js` para chamar funções dentro do chaincode `fabcar`. Essas funções permitem criar e transferir ativos no livro-razão do blockchain. Este tutorial usa a função `initLedger` para incluir novos dados em seu canal e, em seguida, usa o arquivo `query.js` para consultar os dados.

### Chamando o Chaincode
{: #dev-app-invoke}

Abra o arquivo `invoke.js` em um editor de texto.

1. Inclua `var creds = require('./creds.json')` na parte superior do arquivo. Essa linha de código permite que o arquivo `invoke.js` leia informações do arquivo de credenciais `creds.json`.

2. Use a classe [Fabric Client](https://fabric-sdk-node.github.io/Client.html){: external} para configurar a rede de malha usando os terminais de API de seus recursos de rede. Essa etapa define o canal e os peers para os quais seu cliente enviará a proposta, além do serviço de ordenação para o qual o SDK enviará, então, a transação endossada. ** Edite **  o bloco de código relevante abaixo. A linha `creds.peers["org1-peer1"].url` importa a URL do peer de seu arquivo de credenciais.
  ```
  # setup the fabric network
  var channel = fabric_client.newChannel('defaultchannel');
  var peer = fabric_client.newPeer(creds.peers["org1-peer1"].url, { pem: creds.peers["org1-peer1"].tlsCACerts.pem , 'ssl-target-name-override': null});
  channel.addPeer(peer);
  var order = fabric_client.newOrderer(creds.orderers.orderer.url, { pem: creds.orderers.orderer.tlsCACerts.pem , 'ssl-target-name-override': null})
  channel.addOrderer(order);
  ```
  {:codeblock}

  As novas variáveis de peer e de solicitador abrem conexões do gRPC com a sua rede de blockchain. Para obter mais informações sobre o gerenciamento dessas conexões, consulte [Abrindo e fechando conexões de rede](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-app-connections).

  Ao incluir a URL do peer no método `fabric_client.newPeer`, você também importará os certificados TLS relevantes de seu perfil de conexão usando o fragmento de código abaixo. Você fez o mesmo quando incluiu a URL do serviço de ordenação. É necessário usar esses certificados TLS para autenticar a comunicação com a rede.
  ```
  {1}-peer1" ] .tlsCACerts.pem, 'ssl-target-name-override ': null }
  ```
  {:codeblock}

  Se a política de endosso exigir que as transações sejam endossadas por outras organizações no canal, será necessário incluir esses peers de organizações usando os métodos `newPeer()` e `channel.addPeer()` ao configurar a rede. O envio das organizações precisa enviar a você a lista dos peers que foram associados a um canal específico. As informações sobre terminais e os certificados TLS estarão disponíveis no perfil de conexão. O SDK enviará a transação para todos os peers incluídos no canal.

  Também é possível incluir peers adicionais pertencentes à sua organização que foram associados ao canal como uma etapa para [tornar seu aplicativo altamente disponível](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-ha-app). Isso fornecerá ao SDK um failover no caso de um de seus peers ser interrompido.

3. Depois de configurar a rede de malha e importar a identidade do aplicativo e o signCert da etapa de registro, o arquivo `invoke.js` definirá a proposta que você enviará para a rede. É possível usar a função `initLedger` no chaincode `fabcar` para incluir alguns dados iniciais no livro-razão. Também é possível editar o bloco de códigos para chamar outras funções que podem ser localizadas no chaincode `fabcar`.
  ```
  solicitação var = {
    //targets: let default to the peer assigned to the client
    chaincodeId: 'fabcar',
    fcn: 'initLedger',
    args: [''],
    chainId: 'defaultchannel',
    txId: tx_id
  };
  ```
  {:codeblock}

  Depois de definir a solicitação, é possível enviar uma [proposta de transação](https://fabric-sdk-node.github.io/Channel.html#sendTransactionProposal){: external} para os peers no canal. Depois que a proposta é retornada dos peers, é possível [enviar a transação](https://fabric-sdk-node.github.io/Channel.html#sendTransaction){: external} para o serviço de pedido.

4. É possível incluir um serviço de evento para tornar o fluxo de transação mais eficiente. **Edite** a seção a seguir:
  ```
  let event_hub = fabric_client.newEventHub();
  event_hub.setPeerAddr(creds.peers["org1-peer1"].eventUrl, { pem: creds.peers["org1-peer1"].tlsCACerts.pem , 'ssl-target-name-override': null});
  ```
  {:codeblock}

  Embora a amostra use um serviço de evento baseado em peer, é necessário usar um listener baseado em canal. É possível saber mais na seção [Gerenciando transações](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-managing-transactions) e na [documentação do Node SDK](https://fabric-sdk-node.github.io/tutorial-channel-events.html){: external}.

5. Por padrão, `invoke.js` envia a transação como `user1`. Será possível editar o arquivo `invoke.js` se você tiver registrado um nome diferente.

Depois de concluir a edição do arquivo, emita o comando `node invoke.js` para enviar a transação para a rede. A seguinte confirmação de que a chamada foi bem-sucedida deve ser exibida.
```
Successfully sent Proposal and received ProposalResponse: Status - 200, message - "OK"
```

Isso indica que seu aplicativo chamou com sucesso o chaincode e incluiu dados no livro-razão.

### Consultando o chaincode
{: #dev-app-query}

Agora é possível usar `query.js` para ler o livro-razão. Abra o arquivo `query.js` em um editor de texto.

1. Inclua `var creds = require('./creds.json')` na parte superior do arquivo.
2. Atualize o arquivo com o nome do canal e as informações sobre terminais do peer. Como essa operação lê apenas os dados que estão armazenados no peer, não é necessário incluir as informações sobre terminais do serviço de ordenação. `query.js` também assume que você envia a proposta como `user1`.
  ```
  var channel = fabric_client.newChannel('defaultchannel');
  var peer = fabric_client.newPeer(creds.peers["org1-peer1"].url, { pem: creds.peers["org1-peer1"].tlsCACerts.pem , 'ssl-target-name-override': null});
  channel.addPeer(peer);
  ```
  {:codeblock}

Depois de concluir a edição do arquivo, emita o comando `node query.js` e você deverá ver a lista de carros no livro-razão, que é semelhante ao exemplo a seguir.
```
Query has completed, checking results
Response is  
  [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},
  {"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},
  ...
```
{:codeblock}

Para obter mais informações sobre o aplicativo fabcar e as funções que ele usa, é possível visitar o tutorial completo [Escrevendo seu primeiro aplicativo](https://hyperledger-fabric.readthedocs.io/en/release-1.2/write_first_app.html){: external} na Documentação do Hyperledger Fabric.

## Usando seu Perfil de conexão com o SDK
{: #dev-app-connection-profile}

Em vez de importar as informações sobre terminais de sua rede manualmente, é possível fazer com que o SDK se conecte à sua rede usando o **Perfil de conexão** por meio da tela **Visão geral** de seu Monitor de rede. Isso simplifica o processo de conexão com a Autoridade de certificação para inscrição e registro. Também elimina a necessidade de definir sua rede de malha antes de enviar uma transação. O SDK localizará os peers e os solicitadores no canal relevante diretamente do Perfil de conexão. É possível localizar mais informações sobre como usar um perfil de conexão na [Documentação do Node SDK](https://fabric-sdk-node.github.io/tutorial-network-config.html){: external}.

É possível usar o arquivo `invoke.js` como um exemplo para ver a eficiência da utilização de um Perfil de Conexão em vez de terminais manuais. É possível estabelecer uma nova instância do cliente de malha usando a classe `loadFromConfig`. Substitua `var fabric_client = new Fabric_Client();` pelo código a seguir.
```
var fabric_client = Fabric_Client.loadFromConfig (path.join (__dirname, './connection-profile.json'));
```
{:codeblock}

Em vez de configurar a rede de malha criando peers e solicitadores e, em seguida, incluindo-os em um canal, é possível usar a linha a seguir para criar um novo canal.

```
var channel = fabric_client.newChannel ('defaultchannel');
```
{:codeblock}

Em seguida, o SDK inclui os peers e o serviço de ordenação definidos no canal usando o Perfil de conexão. Isso torna a composição de aplicativos mais eficiente e facilita a atualização de seus aplicativos à medida que os membros da rede se associam, saem e iniciam novos canais. Consulte o [tutorial do perfil de conexão](https://fabric-sdk-node.github.io/tutorial-network-config.html){: external} na Documentação do Node SDK para saber mais sobre as etapas adicionais envolvidas. É possível usar essa [versão do tutorial do fabcar](https://developer.ibm.com/tutorials/cl-deploy-fabcar-sample-application-ibm-blockchain-starter-plan/){: external} que usa um perfil de conexão em vez de conexões de terminal manuais.

A[Descoberta de serviço](https://hyperledger-fabric.readthedocs.io/en/release-1.2/discovery-overview.html){: external} para uma política de endosso no Hyperledger Fabric não é suportada para o plano Starter ou o plano Enterprise. No entanto, é possível enviar transações para peers que estão fora de sua organização para endosso, editando seu Perfil de conexão. O Perfil de conexão já contém as informações sobre terminais e os certificados TLS de peers de outras organizações em sua rede do {{site.data.keyword.blockchainfull_notm}} Platform. Inclua o nome do peer no canal relevante na seção "canais" do perfil para incluir o peer no canal. Será necessário entrar em contato com os administradores das outras organizações sobre quais peers eles associaram a canais específicos.

## Gerando certificados usando o Monitor de Rede
{: #dev-app-enroll-panel}

É possível usar o Monitor de Rede para gerar certificados usando a identidade de administrador e, em seguida, transmitir esses certificados diretamente para o SDK. Isso significa que você pode começar a interagir com a rede rapidamente, sem precisar gerar certificados usando o SDK.

Navegue para o painel "Autoridade de certificação" em seu Monitor de Rede. Clique no botão **Gerar certificado** ao lado de sua identidade de administrador para obter um novo signCert e uma chave privada de sua CA. O campo **Certificado** contém o signCert, logo acima da **Chave privada**. É possível clicar no ícone de cópia no final de cada campo para copiar o valor. Salve esses certificados em um local em que é possível fornecê-los ao seu aplicativo. **Observe** que o {{site.data.keyword.blockchainfull_notm}} Platform não armazena esses certificados. Você precisará salvar e armazená-los com segurança.

O signCert e a chave privada são suficientes para formar um contexto de usuário que possa assinar solicitações dentro do Node SDK. Use o método [createUser](https://fabric-sdk-node.github.io/Client.html#createUser__anchor){: external} da classe Client para criar o objeto de contexto do usuário. No método `creatUser`, passe o nome de identidade e mspid para o objeto [user](https://fabric-sdk-node.github.io/global.html#UserOpts){: external}, juntamente com os caminhos para a chave privada e signCert para o objeto [cryptoContent](https://fabric-sdk-node.github.io/global.html#CryptoContent){: external}.

É possível usar o painel "Autoridade de certificação" e a classe `createUser` como parte do tutorial de desenvolvimento de aplicativos como um exemplo. Se você já tiver passado pelo tutorial, você instalou e instanciou o chaincode `fabcar` e incluiu alguns dados em seu livro-razão. É possível usar os certificados para consultar o livro-razão como o usuário `admin`. Siga as instruções para gerar certificados usando o Monitor de Rede acima, se você ainda não tiver feito isso.

Salve sua chave privada como privateKey.pem e sua signCert como certificate.pem no mesmo diretório que `query.js`. Abra `query.js` em um editor de texto. Inclua a linha a seguir no início do arquivo:
```
var fs = require('fs');
```
Substitua a linha a seguir que importa o contexto do usuário de persistência,
```
return fabric_client.getUserContext('user1', true);
```
pelo código a seguir que cria um novo contexto do usuário usando nosso signCert e a chave privada.
```
return fabric_client.createUser({
		username: 'admin',
		mspid:  'org1',
		cryptoContent: {
			privateKeyPEM: fs.readFileSync(path.join(__dirname,'./privateKey.pem')),
			signedCertPEM: fs.readFileSync(path.join(__dirname,'./certificate.pem'))
		}});
```
O snippet acima lê seus certificados diretamente para a classe `cryptoContent` como arquivos PEM. O nome de usuário será `admin`, uma vez que os certificados foram gerados usando a identidade `admin`. É possível localizar seu mspid na seção `certificateAuthorites` de seu perfil de conexão. Salve o arquivo e emita o comando `node query.js`. Se bem-sucedida, a consulta retornará os mesmos resultados de antes.

## (Opcional) Operando sua rede usando o SDK
{: #dev-app-operate-sdk}

Também é possível usar o SDK para operar sua rede de blockchain. Este tutorial explica como é possível usar o SDK para associar os peers a canais, instalar o chaincode nos peers e instanciar o chaincode em canais. Essas etapas serão opcionais porque também será possível executar essas operações usando o Monitor de rede ou as APIs na [IU do Swagger](/docs/services/blockchain/howto?topic=blockchain-ibp-swagger#ibp-swagger) se todos os peers estiverem sendo executados no {{site.data.keyword.blockchainfull_notm}} Platform.

É necessário fazer upload do signCert do administrador para o {{site.data.keyword.blockchainfull_notm}} Platform para concluir essas etapas. É possível localizar instruções sobre como fazer upload do signCert no final da [seção de inscrição](#dev-app-enroll-sdk)

### Unindo um canal
{: #dev-app-join-channel-sdk}

Depois que sua organização criar ou associar-se a um canal usando o Monitor de Rede ou as APIs, será possível usar o SDK para associar seu peer ao canal.

1. [Busque o bloco genesis](https://fabric-sdk-node.github.io/Channel.html#getGenesisBlock){: external} do canal por meio do serviço de pedido.
2. Passe o bloco genesis para o método [join channel](https://fabric-sdk-node.github.io/Channel.html#joinChannel){: external} para associar seu peer ao canal.

Para usar a amostra `fabcar` para associar um canal, use o arquivo `invoke.js` como seu ponto de início. Você precisará enviar essa solicitação como o administrador em vez do aplicativo, portanto, substitua `user1` por `admin` no método `getUserContext`. Começando onde você define o seu chaincode, chame a solicitação em `var request = {` e substitua o fluxo de transação por uma solicitação de associação de canal com base no fragmento de código na [Documentação do Node SDK](https://fabric-sdk-node.github.io/tutorial-channel-create.html){: external}.
  ```
  let g_request = {
    txId :     tx_id
  };

  // get the genesis block from the orderer
  channel.getGenesisBlock(g_request).then((block) =>{
    genesis_block = block;
    tx_id = client.newTransactionID();
    let j_request = {
      targets : targets,
      block : genesis_block,
      txId :     tx_id
    };
    // send genesis block to the peer
    return channel.joinChannel(j_request);
  }).then((results) =>{
    if (resultados & & results [ 0 ] .response & & results [ 0 ] .response.status == 200) {
    // good  
    } else {
      // not good
    }
  });
  ```

Seu signCert precisa ser incluído no canal antes que você possa buscar o bloco genesis. Se você gerou certificados depois que sua organização se associou ao canal, será necessário fazer upload de seu signCert para a plataforma e, em seguida, clicar no botão **Sincronizar certificados** na tela "Canais". Talvez seja necessário aguardar alguns minutos para que a sincronização do canal seja concluída antes de emitir o comando de canal de junção. Para obter mais informações, veja [Fazendo upload de certificados de assinatura para o {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates-upload-certs) no tutorial [Gerenciando certificados](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates).

### Instalando um chaincode
{: #dev-app-install-cc-sdk}

É possível usar o método [install chaincode](https://fabric-sdk-node.github.io/Client.html#installChaincode){: external} por meio da classe [Fabric Client](https://fabric-sdk-node.github.io/Client.html){: external} para instalar o chaincode em seu peer.

Para usar a amostra `fabcar` para instalar o chaincode `fabcar` no peer, use o arquivo `query.js` como uma linha de base e edite-o. Você precisará enviar essa solicitação como o administrador em vez do aplicativo, portanto, substitua `user1` por `admin` no método `getUserContext`. Substitua o objeto de proposta da transação por uma solicitação de chaincode de instalação usando o exemplo a seguir:
```
solicitação var = {
    targets: peer,
    chaincodePath: chaincode_path,
    chaincodeId: 'fabcar',
    chaincodeType: 'golang',
    chaincodeVersion: 'v1',
    channelNames: 'defaultchannel'
	 };
```
{:codeblock}

Envie esse objeto para `return fabric_client.installChaincode(request);`, em vez da linha `return channel.queryByChaincode(request);` atualmente no arquivo.

### Instanciando um Chaincode
{: #dev-app-instantiate-cc-sdk}

Para instanciar o chaincode, é necessário enviar uma [proposta de instanciação](https://fabric-sdk-node.github.io/Channel.html#sendInstantiateProposal){: external} para o peer e, em seguida, enviar uma [solicitação de transação](https://fabric-sdk-node.github.io/Channel.html#sendTransaction){: external} para o serviço de pedido.

Para usar a amostra `fabcar` para instanciar seu chaincode, use o arquivo `invoke.js` como seu ponto de início. Você precisará enviar essa solicitação como o administrador em vez do aplicativo, portanto, substitua `user1` por `admin` no método `getUserContext`. Substitua o objeto de proposta da transação por uma solicitação de chaincode de instalação usando o exemplo a seguir:
```
solicitação var = {
    targets: peer,
    chaincodePath: chaincode_path,
    chaincodeId: 'fabcar',
    chaincodeType: 'golang',
    chaincodeVersion: 'v1',
    channelNames: 'defaultchannel',
    txId : tx_id
};
```
{:codeblock}

Envie esta solicitação para `return channel.sendInstantiateProposal(request);` em vez de `return channel.sendTransactionProposal(request);` atualmente no arquivo. Depois de enviar a solicitação de instanciação para o canal, será necessário enviar a proposta endossada como uma transação para o serviço de ordenação. São usados os mesmos métodos que o envio de uma transação, portanto, é possível manter o restante do arquivo sem mudanças. Você pode desejar [aumentar o valor de tempo limite](/docs/services/blockchain?topic=blockchain-best-practices-app#best-practices-set-timeout-in-sdk) na proposta de instanciação. Caso contrário, a solicitação poderá atingir o tempo limite antes que a plataforma possa iniciar o contêiner de chaincode.

Seu signCert precisa ser incluído no canal antes de poder instanciar o chaincode. Se você gerou certificados depois de entrar no canal, será necessário fazer upload de seu signCert para a plataforma e, em seguida, clicar no botão **Sincronizar certificados** na tela "Canais". Talvez seja necessário aguardar alguns minutos para que a sincronização do canal seja concluída antes de emitir o comando instantiate chaincode. Para saber mais, consulte [Fazendo upload de certificados de assinatura para o {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates-upload-certs) no tutorial [Gerenciando certificados](/docs/services/blockchain?topic=blockchain-managing-certificates#managing-certificates).

## Desconectando seu aplicativo da rede
{: #dev-app-disconnect-app}

Conclua as etapas a seguir para remover a conexão entre seu aplicativo e a rede de blockchain no {{site.data.keyword.cloud_notm}}.
1. Remova as informações do terminal da API de seu arquivo de configuração do aplicativo. Para referência, consulte [Incluindo terminais de API de rede em seu aplicativo](#dev-app-api-endpoints).
2. Exclua seu contêiner de chaincode.
  1. Na tela "Canal" do Monitor de Rede, localize o canal no qual o chaincode está instalado.
  2. Na tela do canal específico, localize o chaincode que deseja desativar.
  3. Clique no botão **Excluir** e clique em **Enviar** no painel de exclusão do chaincode. O seu contêiner do chaincode será removido.
	![Excluir um chaincode](images/channel_chaincode.png "Excluir um chaincode")
