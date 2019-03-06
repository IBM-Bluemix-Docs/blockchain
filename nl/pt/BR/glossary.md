---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Glossário
{: #glossary}

***[Esta página é útil? Diga-nos.](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***

Este tópico define {{site.data.keyword.blockchainfull}}Termos específicos da plataforma que aparecem nesta documentação. Para um entendimento mais profundo dos termos e para obter um glossário de termos relacionados aos conceitos do Hyperledger Fabric, consulte o [Glossário do Hyperledger Fabric ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](http://hyperledger-fabric.readthedocs.io/en/release-1.2/glossary.html).
{:shortdesc}

## Ativo
{: #glossary-asset}
Bens tangíveis ou intangíveis, serviços ou propriedade que são representados como um item que é negociado na rede de blockchain.

## Atrib
{: #glossary-block}
Um conjunto ordenado de transações, que é criptograficamente vinculado ao bloco anterior em um canal.

## Rede de negócios
{: #glossary-business-network}
Uma definição de uma rede de blockchain, que inclui o modelo de dados, a lógica de transação e as regras de controle de acesso para a sua solução de blockchain. Definições de rede de negócios são criadas usando o [Hyperledger Composer](/docs/services/blockchain/glossary.html#glossary-composer). Definições de rede de negócios são empacotadas em arquivos **.bna** (archive de rede de negócios) implementáveis.

## CA
{: #glossary-CA}
Uma abreviação de "Autoridade de Certificação", esse é o componente que emite certificados para todos os membros participantes. Esses certificados representam a identidade de um membro. Todas as entidades na rede (peers, solicitantes, clientes etc.) deve ter uma identidade para se comunicar, autenticar e, finalmente, transacionar. Essas identidades são necessárias para qualquer participação direta na rede de blockchain.

## Cadeia
{: #glossary-chain}
A cadeia do livro-razão é um log de transações estruturado como blocos de transações vinculados ao hash. Peers recebem blocos de transações do serviço de ordenação, marcam as transações do bloco como válidas ou inválidas com base em políticas de aprovação e violações de simultaneidade e anexam o bloco à cadeia hash no sistema de arquivos do peer.

## Chaincode
{: #glossary-chaincode}

Também conhecido como **contratos inteligentes**, o chaincode são as partes do software que contêm um conjunto de funções para consultar ou atualizar o livro-razão.

## Canal
{: #glossary-channel}
Consiste de um subconjunto de membros de rede que querem transacionar em particular. Os canais fornecem isolamento de dados e confidencialidade permitindo que os membros de um canal estabeleçam regras específicas e um livro-razão separado que somente membros do canal podem acessar. Peers, que são os nós que funcionam como os terminais de transação para organizações, são unidos aos canais.

## Cliente
{: #glossary-client}
O cliente representa a entidade que age em nome de um usuário. Ele deve se conectar a um peer para comunicação com o blockchain. O cliente pode se conectar a qualquer peer de sua escolha. Os clientes criam e, assim, chamam transações. O cliente envia uma chamada de transação real para os endossantes e transmite propostas de transação para o serviço de ordenação.

## Perfil de conexão
{: #glossary-connection-profile}
O perfil de conexão é visível na tela "Visão geral" do Monitor de rede quando você clica no botão **Perfil de conexão**. As informações estão disponíveis no formato JSON e contêm as informações de terminal de API e enrollIDs/segredos para os seus recursos de rede, ou seja, peers, solicitantes e autoridades de certificação. O seu aplicativo interage com recursos de rede por meio desses terminais de API.

## Consenso
{: #glossary-consensus}
Um processo colaborativo para manter as transações o livro-razão sincronizadas na rede. O consenso assegura que os livros-razão são sejam atualizados apenas quando os participantes apropriados aprovam transações e que isso seja feita com as mesmas transações na mesma ordem. Existem muitas formas algorítmicas diferentes de alcançar o consenso.

## Consórcio
{: #glossary-consortium}
O grupo de organizações não solicitadoras listadas no canal do sistema do solicitador. Essas são as únicas organizações que podem criar canais. No momento da criação do canal, todas as organizações incluídas no canal devem fazer parte de um consórcio. No entanto, uma organização que não esteja definida em um consórcio poderá ser incluída em um canal existente. Embora uma rede de blockchain possa ter vários consórcios, a maioria das redes de blockchain tem um único consórcio.

## CouchDB
{: #glossary-couchdb}
Um armazenamento de documentos usado para o banco de dados de estado nas redes do Starter Plan. O CouchDB também é uma opção para redes do Enterprise Plan, juntamente com o LevelDB. O CouchDB suporta o uso de índices e permite emitir consultas complexas com relação aos dados em seu peer.

## Estado atual
{: #glossary-current-state}

O estado atual do livro-razão representa os valores mais recentes para todas as chaves já incluídas em seu log de transações de cadeia. Como o estado atual representa todos os valores da chave mais recentes conhecidos para o canal, ele é, às vezes, referido como um Estado mundial. O chaincode executa propostas de transação com relação a dados de estado atuais. O estado atual muda sempre que o valor de uma chave muda ou que uma nova chave é incluída. O estado atual é crítico para um fluxo de transação porque o último par chave-valor deve ser conhecido antes de poder ser mudado. Os peers confirmam os valores mais recentes para o estado atual do livro-razão para cada transação válida em um bloco. O estado Atual é armazenado no banco de dados de estado de um peer

## Associação dinâmica
{: #glossary-dynamic-memership}
Um membro pode ser incluído dinamicamente na rede por um usuário com privilégio de **escrivão**. Os membros também têm
atribuições e atributos designados, que controlam o seu acesso e autoridade na rede. Apesar disso, nem funções, nem atributos podem ser designados dinamicamente. O Hyperledger Fabric suporta a inclusão ou remoção de membros, peers e nós de serviço de ordenação, sem comprometer as operações da rede geral. A associação dinâmica é crítica quando os relacionamentos de negócios se ajustam e as entidades precisam ser incluídas ou removidas por vários motivos.

## Aprovação
{: #glossary-endorsement}
O processo pelo qual as transações de chaincode são validadas. Regras de aprovação são implementadas especificando as políticas de aprovação.

## Política de aprovação
{: #glossary-endorsement-policy}
Define os nós de peer em um canal que deve executar transações que estão conectadas a um aplicativo de chaincode específico e a combinação necessária de respostas (aprovações). Uma política pode requerer que uma transação seja endossada por um número mínimo de peers de aprovação, uma porcentagem mínima de peers ou por todos os peers que são designados a um aplicativo de chaincode específico. As políticas podem ser curadas com base no aplicativo e no nível desejado de resiliência com relação a mau comportamento, se deliberado ou não, pelo peers de aprovação. Uma transação enviada deve satisfazer a política de aprovação antes de ser marcada como válida por peers de confirmação. Uma política de aprovação distinta para instalar e instanciar transações também é necessária.

## Bloco genesis
{: #glossary-genesis-block}
O bloco de configuração que inicializa uma rede de blockchain ou canal e também serve como o primeiro bloco em uma cadeia.

## Fofoca
{: #glossary-gossip}
O Hyperledger Fabric permite que os peers reúnam informações importantes de rede entre si sem ter que depender do serviço de ordenação. O [protocolo de disseminação de dados de fofoca ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.1/gossip.html) fornece uma maneira segura, confiável e escalável para os peers trocarem mensagens entre si. Por exemplo, se os peers perderem alguns blocos devido a atrasos, indisponibilidades de rede ou outros motivos, eles poderão sincronizar-se com o estado atual do livro-razão usando o sistema de mensagens de fofoca para entrar em contato com outros peers que tiverem a posse desses blocos ausentes.

## HSM
{: #glossary-hsm}
Hardware Security Module. Fornece criptografia on demand, gerenciamento de chave e armazenamento de chave como um serviço gerenciado. HSM é um dispositivo físico que manipula as tarefas intensivas em recurso de processamento de criptografia e reduz a latência para aplicativos. Para obter mais informações, veja [Hardware Security Module ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](https://www.ibm.com/cloud/hardware-security-module)

## Editor do Hyperledger
{: #glossary-composer}
**A IBM não fornece suporte para redes que usam o Hyperledger Composer na produção, incluindo a CLI do Composer, as APIs JavaScript, o servidor REST e o Web Playground.**
[Hyperledger Composer ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](https://hyperledger.github.io/composer/latest/introduction/introduction.html) é um conjunto de ferramentas de desenvolvimento de software livre. Ele usa uma linguagem de modelagem sob medida, que é combinada com transações do JavaScript e regras de controle de acesso para modelar uma rede de negócios de blockchain na íntegra. É possível usar o Hyperledger Composer para integrar sistemas e dados existentes ao seu aplicativo de blockchain antes de implementar qualquer coisa em um blockchain real.

## Hyperledger Fabric
{: #glossary-hyperledger-fabric}
[Hyperledger Fabric ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](http://hyperledger-fabric.readthedocs.io/en/release-1.1/) é uma estrutura de blockchain de negócios que a Fundação Linux hospeda para servir como uma base para desenvolver aplicativos de blockchain ou soluções com uma arquitetura modular. Componentes do Hyperledger Fabric como serviços de consenso e de associação são plug-and-play.

## Instalar
{: #glossary-install}
O processo de colocar um chaincode no sistema de arquivos de um peer. Deve-se instalar o chaincode em cada peer que executará esse chaincode.

## Instanciar
{: #glossary-instantiate}
O processo de iniciar e inicializar um contêiner de chaincode em um canal específico. Após o chaincode ser instalado nos Peers e cada Peer ter se associado ao canal, o chaincode deverá ser instanciado no canal. A instanciação executa qualquer inicialização necessária do chaincode, que inclui configurar os pares de chave-valor que constituem o estado geral inicial do chaincode. Após a instanciação, peers que tiverem o chaincode instalado poderão aceitar chamadas de chaincode.

## Kafka
{: #glossary-kafka}
Uma implementação de plug-in de consenso para o Hyperledger Fabric que resulta em um cluster de nós de serviço de ordenação na rede de blockchain. Uma implementação Kafka é destinada a uma rede de produção.

## Livro-razão
{: #glossary-ledger}
Composto por uma "cadeia de blocos" literal que armazena o registro sequencial imutável de transações, bem como um banco de dados de estado para manter o estado atual. Há um livro-razão por canal e as atualizações para ele são gerenciadas pelo processo de consenso de acordo com as políticas de um canal específico.

## LevelDB
{: #glossary-leveldb}
Um armazenamento de valor de chave que é uma opção para o banco de dados de estado para redes do Enterprise Plan, junto ao CouchDB. O LevelDB armazena o estado atual como pares de valor da chave e não suporta o uso de índices ou consultas complexas.

## Membro
{: #glossary-member}

Também conhecidos como "organizações", os membros em uma rede de blockchain, semelhantes aos membros de qualquer grupo, formam a estrutura da rede. Um membro pode ser tão grande quanto uma corporação multinacional ou tão pequeno quanto um indivíduo. Os membros são inscritos na rede com um certificado que lhes concede permissões para usar a rede como um provedor de serviços (por exemplo, emissão de certificados, validação/solicitação de transações) ou como um consumidor. O primeiro fornece serviços básicos de blockchain que incluem validação de transação, solicitação de transação e serviços de gerenciamento de certificado. Os membros do consumidor usam a rede para chamar transações com relação ao livro-razão distribuído. Os membros podem ter múltiplos Peers.

## MSP
{: #glossary-msp}
Membership Service Provider.  Um conjunto de mecanismos e protocolos criptográficos para emissão e validação de certificados e identidades em toda a rede de blockchain. Identidades que são emitidas no escopo de um provedor de serviços de associação podem ser avaliadas dentro das políticas de validação de regras do provedor de serviços dessa associação. O MSP é instalado em cada peer de canal para assegurar que as solicitações de transação que são emitidas para o peer se originem de uma identidade do usuário autenticada e autorizada.

## Rede
{: #glossary-network}
Uma instância de um serviço do {{site.data.keyword.blockchainfull_notm}} Platform no {{site.data.keyword.cloud_notm}}.

## Credenciais de rede
{: #glossary-network-credentials}
Visível da tela "APIs" do Monitor de rede. As credenciais incluem a sua "chave" (Nome do usuário) e o "segredo" (Senha) na UI do Swagger. É necessário usar essas credenciais de rede para autenticar antes de tentar as APIs de REST.

## Monitor de rede
{: #glossary-network-monitor}
O painel da GUI que o {{site.data.keyword.blockchainfull_notm}} Platform fornece para visualizar e gerenciar a rede de blockchain.

## Nó
{: #glossary-node}
A entidade de comunicação do blockchain. Há três tipos de nós: CA, Peer e solicitador.

## Solicitador
{: #glossary-orderer}
O nó que coleta transações de membros da rede, ordena as transações e as empacota em blocos. Esses blocos são, então, distribuídos para os peers que, em seguida, verificam os blocos e os incluem nos livros-razão em cada canal. Os solicitadores contêm o material de identidade criptográfica que está vinculado a cada membro e autenticam a identidade de clientes e peers para acesso à rede. A função geral que um nó de solicitação ou coleta de nós fornece é conhecida como o **serviço de ordenação**.

## Organização
{: #glossary-organization}
Veja [Membro](/docs/services/blockchain/glossary.html#glossary-member).

## Participante
{: #glossary-participant}
Qualquer organização, indivíduo, aplicativo ou dispositivo que interaja com a rede de blockchain. Sob o guarda-chuva de participante há dois agrupamentos distintos, que são membros e usuários.

## Peer
{: #glossary-peer}
Um recurso de rede de blockchain que fornece os serviços para executar e validar transações e manter livros-razão. O Peer executa o chaincode e é o portador do histórico de transação e o estado atual de ativos nos canais da rede, ou seja, o livro-razão. Eles são de propriedade e gerenciados por organizações e são associados a canais.

## Credenciais de serviço
{: #glossary-service-credentials}
As credenciais de serviço estão no formato JSON e contêm as informações de terminal da API e os enrollIDs/segredos para seus recursos de rede, ou seja, autoridades de certificação, solicitadores e peers. O seu aplicativo interage com recursos de rede por meio desses terminais de API.

## SDK
{: #glossary-sdk}
O Hyperledger Fabric suporta dois Software Development Kits (SDKs). Um SDK do Nó e SDK do Java.  O SDK do Nó pode ser instalado via NPM e o SDK do Java via Maven.  Os SDKs têm os seus próprios repositórios Git, ou seja, [Fabric Node SDK ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](https://github.com/hyperledger/fabric-sdk-node) e [Fabric Java SDK ![Ícone de link externo](images/external_link.svg "Ícone de link externo")](https://github.com/hyperledger/fabric-sdk-java), com a documentação para as APIs disponíveis. Os SDKs do Hyperledger Fabric Client permitem a interação entre o seu aplicativo cliente e a sua rede de blockchain.

## SignCert
{: #glossary-sign-cert}
O certificado que quaisquer entidades, sejam organizações ou administradores, anexam às suas propostas ou respostas de proposta. Esses signCerts são exclusivos de uma entidade e são verificados pelo serviço de ordenação para garantir que eles correspondam ao signCert no arquivo para essa entidade.

## Contratos inteligentes
{: #glossary-smart-contracts}
Consulte [Chaincode](/docs/services/blockchain/glossary.html#glossary-chaincode).

## SOLO
{: #glossary-solo}
Uma implementação de plug-in de consenso para o Hyperledger Fabric que resulta em um único nó de serviço de ordenação na rede de blockchain. A rede do Starter Plan usa a implementação SOLO. Uma implementação SOLO não é destinada para uma rede de produção. A alternativa para SOLO é um cluster do Kafka.

## Banco de dados de
{: #glossary-state-database}
Os dados de estado atual são armazenados em um banco de dados nos peers para leituras eficientes e consultas do chaincode. As redes do Starter Plan usam o CouchDB como o banco de dados de estado. O Enterprise Plan Networks pode usar o LevelDB ou o CouchDB.

## Transação
{: #glossary-transaction}
O mecanismo que participantes na rede de blockchain usam para interagir com ativos. Uma transação cria novo chaincode ou chama uma operação em um chaincode existente.

## Usuário
{: #glossary-user}
Um usuário é um participante em uma rede de blockchain que tem acesso indireto ao livro-razão por meio de um relacionamento de confiança para um membro existente.

## Mundo estado
{: #glossary-world-state}
Consulte [Estado Atual]((/docs/services/blockchain/glossary.html#glossary-current-state).
