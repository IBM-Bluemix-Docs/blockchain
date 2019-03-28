---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-05"

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Glosario
{: #glossary}

En este tema se definen términos específicos de {{site.data.keyword.blockchainfull}} Platform que aparecen en esta documentación. Para estudiar los términos con más detalle y ver un glosario de términos relacionados con los conceptos de Hyperledger Fabric, consulte el [Glosario de Hyperledger Fabric
![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](http://hyperledger-fabric.readthedocs.io/en/release-1.2/glossary.html).
{:shortdesc}

## Activo
{: #glossary-asset}
Bienes, servicios o propiedades tangibles o intangibles que se representan como un elemento con el que se comercia en la red blockchain.

## Bloque
{: #glossary-block}
Conjunto ordenado de transacciones, que está vinculado criptográficamente al bloque anterior en un canal.

## Red empresarial
{: #glossary-business-network}
Definición de una red blockchain, que incluye modelo de datos, lógica de transacción y reglas de control de acceso de la solución blockchain. Las definiciones de red empresarial se crean mediante [Hyperledger Composer](/docs/services/blockchain/glossary.html#glossary-composer). Las definiciones de la Red empresarial se empaquetan en archivos **.bna** (Business Network Archive) que se pueden desplegar.

## CA
{: #glossary-CA}
Abreviatura de "entidad emisora de certificados"; es el componente que emite certificados a todos los miembros participantes. Estos certificados representan la identidad de un miembro. Todas las entidades de la red (iguales, clasificadores, clientes, etc.) deben tener una identidad para comunicarse, autenticarse y realizar transacciones. Estas identidades son necesarias para cualquier participación directa en la red blockchain.

## Cadena
{: #glossary-chain}
La cadena del libro mayor es un registro de transacciones estructurado como bloques de transacciones relacionadas con hash. Los iguales reciben bloques de transacciones del servicio de ordenación, marcan las transacciones del bloque como válidas o no válidas en función de las políticas de aprobación y de las infracciones de simultaneidad y añaden el bloque a la cadena hash en el sistema de archivos del igual.

## Código de encadenamiento
{: #glossary-chaincode}

También conocido como **contratos inteligentes**, el código de encadenamiento son fragmentos de software que contienen un conjunto de funciones para consultar o actualizar el libro mayor.

## Canal
{: #glossary-channel}
Consiste en una subred de miembros de la red que desean realizar transacciones en privado. Los canales proporcionan aislamiento de datos y confidencialidad permitiendo que los miembros de un canal establezcan normas específicas y un libro mayor separado, al que solo pueden acceder los miembros del canal. Los iguales, que son los nodos que funcionan como puntos finales de transacción para las organizaciones, se unen a los canales.

## Cliente
{: #glossary-client}
El cliente representa la entidad que actúa en nombre de un usuario. Debe conectarse a un igual para comunicarse con blockchain. El cliente puede conectarse al igual que desee. Los clientes crean, y por lo tanto invocan, transacciones. El cliente envía una invocación de transacción real a los aprobadores y difunde las propuestas de transacciones al servicio de ordenación.

## Perfil de conexión
{: #glossary-connection-profile}
El archivo de conexión se puede ver en la pantalla "Visión general" del supervisor de red cuando se pulsa el botón **Perfil de conexión**. La información está disponible en formato JSON y contiene la información de punto final de API y los ID de inscripción/secretos de los recursos de la red, es decir, iguales, clasificadores y CA. La aplicación interactúa con los recursos de red a través de estos puntos finales de API.

## Consenso
{: #glossary-consensus}
Proceso de colaboración para mantener las transacciones del libro mayor sincronizadas en la red. El consenso garantiza que los libros mayores se actualizan solo cuando los participantes adecuados apruebas las transacciones y que los libros mayores se actualizan con las mismas transacciones en el mismo orden. Existen muchas maneras algorítmicas diferentes para alcanzar un consenso.

## Consorcio
{: #glossary-consortium}
El grupo de organizaciones que no son de clasificador y que aparecen en el canal del sistema del clasificador. Estas son las únicas organizaciones que pueden crear canales. En el momento de la creación del canal, todas las organizaciones que se añaden al canal deben formar parte del consorcio. No obstante, es posible añadir una organización que no esté definida en un consorcio a un canal existente. Aunque una red blockchain puede tener varios consorcios, la mayoría de las redes blockchain tienen un único consorcio.

## CouchDB
{: #glossary-couchdb}
Un almacén de documentos que se utiliza para la base de datos de estado en las redes del Plan inicial. CouchDB es también una opción para las redes del Plan empresarial, junto con LevelDB. CouchDB soporta el uso de índices y le permite emitir consultas enriquecidas en los datos de su igual.

## Estado actual
{: #glossary-current-state}

El estado actual del libro mayor representa los valores más recientes para todas las claves alguna vez incluidas en su registro de transacciones de encadenamiento. Dado que el estado actual representa todos los valores de claves más recientes conocidos en el canal, a veces se refiere al mismo como Escenario mundial. El código de encadenamiento ejecuta propuestas de transacción en los datos de estado actuales. El estado actual cambia cada vez cuando cambia el valor de una clave o cuando se añade una clave nueva. El estado actual es fundamental para un flujo de transacciones porque el valor clave-valor más reciente debe ser conocido para poder cambiarse. Los iguales confirman los valores más recientes en el estado actual del libro mayor para cada transacción válida de un bloque. El estado Actual se almacena en una base de datos de libro mayor de iguales

## Pertenencia dinámica
{: #glossary-dynamic-memership}
Un usuario con el privilegio de **registrador** puede añadir de forma dinámica un miembro a la red. A los miembros también se les asignan roles y atributos, que controlan su acceso y autoridad en la red. Sin embargo, ni los roles ni los atributos se pueden asignar de forma dinámica. Hyperledger Fabric permite añadir o eliminar miembros, iguales y nodos de servicio de ordenación sin poner en peligro las operaciones de la red general. La pertenencia dinámica resulta crítica cuando se tienen que añadir o eliminar ajustes de relaciones empresariales y entidades por diversos motivos.

## Aprobación
{: #glossary-endorsement}
Proceso por el que se validan las transacciones del código de encadenamiento. Las reglas de aprobación se implementan mediante la especificación de políticas de aprobación.

## Política de aprobación
{: #glossary-endorsement-policy}
Define los nodos iguales de un canal que deben ejecutar las transacciones que están conectadas a una aplicación específica de código de encadenamiento y la combinación de respuestas necesaria (aprobaciones). Una política podría requerir que una transacción sea aprobada por un número mínimo de iguales de aprobación, por un porcentaje mínimo de iguales de aprobación o por todos los iguales de aprobación asignados a una determinada aplicación de código de encadenamiento. Las políticas se pueden definir en función de la aplicación y del nivel deseado de resiliencia frente a un comportamiento inadecuado, ya sea deliberado o no, por parte de los iguales de aprobación. Una transacción enviada debe satisfacer la política de aprobación para que los iguales de confirmación la marquen como válida. También se necesita una política de aprobación distinta para instalar y crear instancias de transacciones.

## Bloque de origen
{: #glossary-genesis-block}
El bloque de configuración que inicializa una red blockchain o canal, y que también sirve como primer bloque en una cadena.

## Gossip
{: #glossary-gossip}
Hyperledger Fabric permite a los iguales recopilar información de red importante entre sí sin tener que depender del servicio de ordenación. El [protocolo de diseminación de datos de rumores (gossip)![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.1/gossip.html) ofrece una forma segura, fiable y escalable de intercambiar mensajes entre sí. Por ejemplo, si los iguales pierden algunos bloques debido a retrasos, cortes de red u otras razones, pueden sincronizarse con el estado del libro mayor actual utilizando la mensajería de rumores para ponerse en contacto con otros iguales que están en posesión de estos bloques que faltan.

## HSM
{: #glossary-hsm}
Módulo de seguridad de hardware (Hardware Security Module). Proporciona funciones de cifrado bajo demanda, gestión de claves y almacenamiento de claves como un servicio gestionado. HSM es un dispositivo físico que maneja las tareas que consumen muchos recursos del proceso de cifrado y que reduce la latencia para las aplicaciones. Para obtener más información, consulte [Módulo de seguridad de hardware ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/cloud/hardware-security-module)

## Hyperledger Composer
{: #glossary-composer}
**IBM no proporciona soporte para redes que utilicen Hyperledger Composer en producción, incluyendo la CLI de Composer, las API de JavaScript, el servidor REST y Web Playground.**
[Hyperledger Composer ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger.github.io/composer/latest/introduction/introduction.html) es un conjunto de herramientas de desarrollo de código abierto. Utiliza un lenguaje de modelado adaptado, que se combina con las transacciones JavaScript, y reglas de control de acceso para modelar una red empresarial de blockchain en su totalidad. Puede utilizar Hyperledger Composer para integrar los sistemas y datos existentes con la aplicación blockchain antes de desplegar nada en un blockchain real.

## Hyperledger Fabric
{: #glossary-hyperledger-fabric}
[Hyperledger Fabric ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](http://hyperledger-fabric.readthedocs.io/en/release-1.1/) es una infraestructura de blockchain empresarial que aloja Linux Foundation para que actúe como base para desarrollar aplicaciones blockchain o soluciones con una arquitectura modular. Los componentes de Hyperledger Fabric, como los servicios de consenso y de pertenencia, son de tipo conectar y listo.

## Instalar
{: #glossary-install}
Proceso de colocar un código de encadenamiento en el sistema de archivos en un igual. Debe instalar el código de encadenamiento en cada igual que vaya a ejecutar dicho código de encadenamiento.

## Crear instancia
{: #glossary-instantiate}
Proceso de iniciar e inicializar un contenedor de código de encadenamiento en un canal específico. Una vez se ha instalado el código de encadenamiento en los iguales y cada igual se ha unido al canal, se debe crear una instancia del código de encadenamiento en el canal. La creación de una instancia realiza la inicialización necesaria del código de encadenamiento, lo que incluye definir los pares de clave y valor que forman el estado inicial de un código de encadenamiento. Después de crear la instancia, los iguales que tienen el código de encadenamiento instalado pueden aceptar invocaciones de código de encadenamiento.

## Kafka
{: #glossary-kafka}
Implementación de plug-in de consenso para Hyperledger Fabric que da lugar a un clúster de nodos de servicio de ordenación en la red blockchain. Una implementación Kafka está pensada para una red de producción.

## Libro mayor
{: #glossary-ledger}
Consta de una "cadena de bloques" literal que almacena el registro de transacciones inmutable y secuencial, así como una base de datos de estado que permite mantener el estado actual. Hay un libro mayor por canal y las actualizaciones en el mismo se gestionan mediante el proceso de consenso según las políticas de cada canal.

## LevelDB
{: #glossary-leveldb}
Un almacén de valor de claves que es una opción para la base de datos de estado para redes del Plan empresarial, junto con CouchDB. LevelDB almacena el estado actual como pares de clave-valor, y no admite el uso de índices ni de consultas enriquecidas.

## Miembro
{: #glossary-member}

También conocidos como "organizaciones", los miembros de una red blockchain, de forma similar a los miembros de cualquier grupo, forman la estructura de la red. Un miembro puede ser tan grande como una empresa multinacional o tan pequeño como un individuo. Los miembros se inscriben en la red con un certificado que les otorga permisos para utilizar la red como un proveedor de servicios (por ejemplo, para emitir certificados o validar y ordenar transacciones) o como un consumidor. El primero proporciona servicios básicos de blockchain que incluyen validación de transacciones, ordenación de transacciones y servicios de gestión de certificados. Los miembros consumidores utilizan la red para invocar transacciones sobre el libro mayor distribuido. Los miembros pueden tener varios iguales.

## MSP
{: #glossary-msp}
Proveedor de servicios de pertenencia (Membership Service Provider).  Conjunto de mecanismos y protocolos de cifrado para emitir y validar certificados e identidades en la red blockchain. Las identidades que se emiten en el ámbito de un proveedor de servicios de pertenencia se pueden evaluar con las políticas de validación de las reglas del proveedor de servicios de pertenencia. El componente MSP se instala en cada igual de canal para garantizar que las solicitudes de transacción que se emiten al igual proceden de una identidad de usuario autorizada y autenticada.

## Red
{: #glossary-network}
Instancia de un servicio de {{site.data.keyword.blockchainfull_notm}} Platform en {{site.data.keyword.cloud_notm}}.

## Credenciales de red
{: #glossary-network-credentials}
Visibles desde la pantalla "API" del supervisor de red. Las credenciales incluyen su "clave" (nombre de usuario) y "secreto" (contraseña) en la IU de Swagger. Debe utilizar estas credenciales de red para autenticarse antes de ejecutar las API REST.

## Supervisor de red
{: #glossary-network-monitor}
Panel de control de GUI que proporciona {{site.data.keyword.blockchainfull_notm}} Platform para ver y gestionar la red blockchain.

## Nodo
{: #glossary-node}
Entidad de comunicación de blockchain. Hay tres tipos de nodos: CA, igual y clasificador.

## Clasificador
{: #glossary-orderer}
El nodo que recopila transacciones de los miembros de la red, ordena las transacciones y las empaqueta en bloques. A continuación, se distribuyen estos bloques a los iguales, que verificarán luego los bloques y los añadirán a los libros mayores de cada canal. Las clasificadores contienen el material de identidad de cifrado que está vinculado a cada miembro y autentican la identidad de clientes e iguales para que puedan acceder a la red. La función global que proporciona un nodo o una recopilación de nodos clasificadores se conoce como **servicio de ordenación**.

## Organización
{: #glossary-organization}
Consulte [Miembro](/docs/services/blockchain/glossary.html#glossary-member).

## Participante
{: #glossary-participant}
Cualquier organización, individuo, aplicación o dispositivo que interactúa con la red blockchain. Bajo el término participante se distinguen dos grupos: los miembros y los usuarios.

## Igual
{: #glossary-peer}
Recurso de la red blockchain que proporciona los servicios para ejecutar y validar transacciones y para mantener libros mayores. El igual ejecuta código de encadenamiento y es el titular del historial de transacciones y del estado actual de los activos en los canales de la red, es decir, del libro mayor. Los iguales son propiedad de las organizaciones, que los gestionan, y se unen a canales.

## Credenciales de servicio
{: #glossary-service-credentials}
Las credenciales de servicio están en formato JSON y contienen la información de punto final de API y los ID de inscripción/secretos de los componentes de red, es decir, CA, clasificadores e iguales. La aplicación interactúa con los recursos de red a través de estos puntos finales de API.

## SDK
{: #glossary-sdk}
Hyperledger Fabric admite dos kits de desarrollo de software (SDK). Un SDK de nodo y un SDK Java.  El SDK de nodo se puede instalar mediante NPM y el SDK Java mediante Maven.  Los SDK tienen sus propios repositorios git, es decir, [SDK de nodo de Fabric ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://github.com/hyperledger/fabric-sdk-node) y [SDK de Java de Fabric ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://github.com/hyperledger/fabric-sdk-java), con documentación sobre las API disponibles. Los SDK de cliente de Hyperledger Fabric permiten la interacción entre la aplicación cliente y la red blockchain.

## SignCert
{: #glossary-sign-cert}
El certificado que las entidades, ya sean organizaciones o administradores, adjuntan a sus propuestas o a sus respuestas a propuestas. Estos signCerts son exclusivos para una entidad y el servicio de ordenación los comprueba para asegurarse de que coinciden con el signCert del archivo para dicha entidad.

## Contratos inteligentes
{: #glossary-smart-contracts}
Véase [Código de encadenamiento](/docs/services/blockchain/glossary.html#glossary-chaincode).

## SOLO
{: #glossary-solo}
Implementación de plug-in de consenso para Hyperledger Fabric que da lugar a un solo nodo de servicio de ordenación en la red blockchain. La red del Plan inicial utiliza la implementación SOLO. La implementación SOLO no está pensada para una red de producción. La alternativa a SOLO es un clúster Kafka.

## Base de datos de estado
{: #glossary-state-database}
Los datos del estado Actual se almacenan en una base de datos de los iguales para lecturas y consultas eficientes del código de encadenamiento. Las redes del Plan inicial utilizan CouchDB como la base de datos de estado. Las redes del Plan empresarial pueden utilizar LevelDB o CouchDB.

## Transacción
{: #glossary-transaction}
Mecanismo que utilizan los participantes en la red blockchain para interactuar con los activos. Una transacción crea código de encadenamiento nuevo o invoca una operación sobre código de encadenamiento existente.

## Usuario
{: #glossary-user}
Un usuario es un participante en una red blockchain que tiene acceso indirecto al libro mayor a través de una relación de confianza con un miembro existente.

## Escenario mundial
{: #glossary-world-state}
Consulte [Estado actual]((/docs/services/blockchain/glossary.html#glossary-current-state).
