---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-23"

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}

# Acerca de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private
{: #ibp-icp-about}

{{site.data.keyword.blockchainfull}} Platform ofrece {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private, que es una plataforma de aplicaciones para desarrollar y gestionar aplicaciones contenerizadas. La oferta {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se basa en Kubernetes, que permite que los usuarios puedan desplegar entidades emisoras de certificados (CA), clasificadores e iguales en x86, LinuxONE e IBM Z. Puede desplegar
{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private utilizando diagramas de Helm de Kubernetes.
{:shortdesc}

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se ha actualizado a Hyperledger Fabric v1.4.0 el 23 de abril de 2019. No obstante, no habrá soporte para datos privados y rumores (gossip) por ahora.
{:note}

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private ofrece los componentes que necesita para ejecutar una red blockchain en su propia infraestructura mediante {{site.data.keyword.cloud_notm}} Private. Los componentes incluyen Hyperledger Fabric, una entidad emisora de certificados (CA), un clasificador y un igual, que puede desplegar, gestionar y configurar utilizando diagramas de Helm de Kubernetes. **Esta oferta está dirigida a los clientes que tengan un nivel alto de experiencia con Hyperledger Fabric.**

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private permite el despliegue de redes blockchain en una nube privada para abordar los requisitos de residencia de datos, las normativas del mercado y las preferencias de infraestructura. Simplifica el despliegue de elementos esenciales de una red blockchain en su propia infraestructura a través de {{site.data.keyword.cloud_notm}} Private, una plataforma de aplicaciones basada en Kubernetes para desarrollar y gestionar aplicaciones contenerizadas locales.

 * Permite que los clientes puedan gestionar redes de {{site.data.keyword.blockchainfull_notm}} Platform con su propia infraestructura. Una edición Community Edition gratuita permite a los clientes realizar la ejecución en sus propios entornos aislados y seguros, pero no se proporciona soporte.
 * Permite que los clientes puedan configurar Fabric en Kubernetes utilizando diagramas de Helm y documentación detallada para las operaciones.
 * Concede a los clientes un soporte técnico avanzado, a menos que utilice Community Edition.

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private es un producto empaquetado para que los clientes de {{site.data.keyword.cloud_notm}} Private puedan desplegar componentes de blockchain en su entorno local. Tras importar el diagrama de Helm, puede encontrarla como un mosaico de {{site.data.keyword.blockchainfull_notm}} Platform en el catálogo de {{site.data.keyword.cloud_notm}} Private. Para obtener más información sobre {{site.data.keyword.cloud_notm}} Private, consulte la documentación para
[{{site.data.keyword.cloud_notm}} Private versión 3.1.2 ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/kc_welcome_containers.html "{{site.data.keyword.cloud_notm}} Private 3.1.2").

## Qué ofrece {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private le permite desplegar todos los componentes fundamentales de un blockchain de Hyperledger Fabric: una entidad emisora de certificados, un servicio de ordenación e iguales. Proporciona la flexibilidad para desplegar distintos componentes según las necesidades empresariales. Puede utilizar {{site.data.keyword.blockchainfull_notm}} para {{site.data.keyword.cloud_notm}} Private para iniciar una red blockchain desplegando y configurando un servicio de ordenación que enlaza organizaciones en un consorcio de blockchain. También puede desplegar iguales y unirse a otras redes que utilicen componentes basados en Fabric, incluyendo redes de {{site.data.keyword.blockchainfull_notm}} Platform desplegadas en nubes utilizando {{site.data.keyword.cloud_notm}} Private o redes de Plan inicial o Plan empresarial alojadas en IBM Cloud. Para obtener más información sobre los bloques de creación de las redes de Hyperledger Fabric, consulte [Visión general de componentes de Blockchain](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview).

## ¿Resulta {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private adecuada para usted?

La ejecución de componentes de {{site.data.keyword.blockchainfull_notm}} Platform fuera de {{site.data.keyword.cloud_notm}} le ofrece una mayor flexibilidad para crecer o unirse a una red blockchain. Resulta de ayuda para que los iniciadores de red hagan crecer sus redes al permitir la unión de nuevos miembros mientras utilizan la plataforma que han elegido. Permitirá que las organizaciones interesadas en unirse a redes blockchain coloquen sus iguales con sus aplicaciones existentes o los integren con sus sistemas de registro.

El proceso para desplegar {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private es complicado y requiere un alto nivel de experiencia en Fabric. Si es nuevo en Fabric, {{site.data.keyword.cloud_notm}} Private o {{site.data.keyword.blockchainfull_notm}} Platform y su objetivo es configurar un entorno de desarrollo o una prueba de concepto, plantéese utilizar el [Plan inicial](/docs/services/blockchain/starter_plan.html#starter-plan-about) en su lugar. Tenga también en cuenta que no todas las configuraciones de despliegue potenciales se admiten en {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private.
{:improtant}

Los usuarios de esta oferta gestionarán su propia seguridad e infraestructura. {{site.data.keyword.cloud_notm}} no ofrece estos servicios. Revise las [Consideraciones y limitaciones](/docs/services/blockchain/ibp-for-icp-about.html#ibp-icp-about-considerations) de la sección siguiente antes de comenzar.

## Consideraciones y limitaciones
{: #ibp-icp-about-considerations}

Antes de empezar, asegúrese de que entiende las **consideraciones** y **limitaciones** siguientes:

- El usuario es responsable de la supervisión del estado, la seguridad, el registro y la gestión del uso de recursos de los componentes.
- Los componentes que se ejecutan en otros entornos de nube no son visibles en el supervisor de red de las redes que se ejecutan en {{site.data.keyword.cloud_notm}}.
- Los diagramas de Helm despliegan una única instancia de un clasificador o igual, o de una CA.
- Puede desplegar varios componentes en un único espacio de nombres en {{site.data.keyword.cloud_notm}} Private, siempre que tengan distintos nombres de release.
- No se pueden direccionar los componentes utilizando la interfaz de usuario de Swagger en la interfaz de usuario del supervisor de red.
- No hay soporte para TLS mutuo.
- La tecnología subyacente, Hyperledger Fabric, utiliza contenedores para ejecutar el código de encadenamiento y Docker para iniciar el contenedor. El único modo para que un igual inicie un contenedor de código de encadenamiento consiste en utilizar Docker-in-Docker, que requiere acceso con privilegios.

**Consideraciones de la entidad emisora de certificados**
- Este diagrama de Helm despliega una única instancia de la CA. Aunque se considera que tener una CA independiente para cada organización es el método recomendado, puede ser necesario desplegar varias CA. Por ejemplo, si tiene pensado desplegar un clasificador y tres iguales, necesitará al menos dos CA (una para la organización del clasificador y otra para la organización del igual).
- Aunque puede optar por ejecutar una base de datos MySQL independiente, esta opción no está presente en el diagrama de Helm. No obstante, el diagrama de Helm desplegará una base de datos SQLite dentro de la CA para gestionar las necesidades de base de datos de la CA, las cuales incluyen la realización del seguimiento del número de inscripciones por usuario y los certificados revocados.

**Consideraciones del clasificador**
- El servicio de ordenación es compatible con cualquier componente en la versión 1.1 o superior de Hyperledger Fabric.
- Este diagrama de Helm despliega una instancia individual del servicio de ordenación SOLO (un clasificador). Tenga en cuenta que no es posible desplegar más de un clasificador SOLO en un canal para hacer que el servicio de ordenación sea de alta disponibilidad. Este es uno de los motivos por los que los servicios de ordenación SOLO son adecuados para entornos de desarrollo, y no para entornos de producción. No obstante, puede desplegar varias instancias del servicio de ordenación SOLO en distintas redes (es decir, con un consorcio independiente).

**Consideraciones del igual**

- Puede conectar los iguales únicamente a redes blockchain que estén en el nivel v1.1 o superior de Fabric. Puede encontrar la versión de Hyperledger Fabric abriendo la [ventana Preferencias de red](/docs/services/blockchain/v10_dashboard.html#ibp-dashboard-network-preferences) en el supervisor de red. Siga las [instrucciones](/docs/services/blockchain/v10_dashboard.html#ibp-dashboard-peer-connection-information) para recuperar la información de conexión del igual de las redes de Plan inicial o empresarial.
- El tipo de base de datos del igual debe coincidir con el tipo de base de datos de la red blockchain, ya sea LevelDB o CouchDB.
- La interfaz CouchDB Fauxton no está disponible en el igual.
- Actualmente no se da soporte a [gossip (rumor)](/docs/services/blockchain/glossary.html#glossary-gossip) para los iguales. Esto implica que tampoco hay soporte para las características de Fabric que dependen de rumores (gossip), como [datos privados ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data-arch.html "datos privados") y [descubrimiento de servicios ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html "descubrimiento de servicios").

## Requisitos previos del sistema
{: #ibp-icp-about-prerequisites}

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private admite los sistemas operativos siguientes:
- Red Hat Enterprise Linux (RHEL) 7.3, 7.4, 7.5
- Ubuntu 18.04 LTS y 16.04 LTS
- SUSE Linux Enterprise Server (SLES) 12 SP3

El diagrama de Helm de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se ha validado para su ejecución en clústeres de {{site.data.keyword.cloud_notm}} Private v3.1.2 en Ubuntu Linux utilizando los nodos trabajadores y el almacenamiento de reserva siguientes:

- **LinuxONE e IBM Z**: z/VM y KVM, que utilizan NFS.
- **x86**: Linux de 64 bits que utiliza GlusterFS.

## Licencias y precios
{: #ibp-icp-about-license-pricing}

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private consta de dos ediciones, una oferta de pago descargable desde Passport Advantage y una edición Community Edition gratuita que está disponible en [GitHub ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://github.com/IBM/charts/tree/master/stable/ibm-blockchain-platform-dev "IBM/charts").

### Licencia
{: #ibp-icp-about-license}

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private proporciona los componentes necesarios para ejecutar una red blockchain en su propia infraestructura y se despliega como una aplicación de {{site.data.keyword.cloud_notm}} Private. Puede acceder a PPA y [descargar el diagrama de Helm](/docs/services/blockchain/howto/helm_install_icp.html#helm-install). El soporte técnico de {{site.data.keyword.blockchainfull_notm}} viene incluido con la compra.

La edición Community Edition de {{site.data.keyword.blockchainfull_notm}} Platform para IBM Cloud Private es una oferta gratuita adecuada para la evaluación y experimentación y se despliega como una aplicación de {{site.data.keyword.cloud_notm}} Private. No utilice Community Edition para producción. {{site.data.keyword.blockchainfull_notm}} Platform no proporciona soporte para Community Edition. Puede acceder al [paquete de GitHub ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://github.com/IBM/charts/blob/master/repo/stable/ibm-blockchain-platform-dev-1.0.2.tgz "IBM/charts") y descargar el diagrama de Helm.

### Precios
{: #ibp-icp-about-pricing}

Los precios de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se basan en el número de núcleos de procesador virtual (VPC) utilizados. Un VPC puede ser un núcleo virtual que se asigna a un servidor virtual, o un núcleo de procesador físico en un servidor no particionado. Debe obtener una titularidad de licencia para cada VPC que se ponga a disposición para la plataforma {{site.data.keyword.blockchainfull_notm}}. <!-- A VPC is a unit of measurement by which a program can be licensed.-->

Para obtener más información sobre cómo determinar su utilización de VPC, consulte este artículo sobre ["Núcleos de procesador virtual (VPC)" ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SS8JFY_9.2.0/com.ibm.lmt.doc/Inventory/overview/c_virtual_processor_core_licenses.html "Núcleos de procesador virtual (VPC)") en {{site.data.keyword.IBM_notm}} Knowledge Center. Puede utilizar la herramienta [{{site.data.keyword.IBM_notm}} License Metric Tool](https://www.ibm.com/support/knowledgecenter/en/SS8JFY_9.2.0/com.ibm.lmt.doc/welcome/LMT_welcome.html) para configurar y crear un informe que puede utilizar para determinar el número de VPC para los que debe obtener una licencia.


## Instalación de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private
{: #ibp-icp-about-install}

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se entrega como un archivo de diagrama de Helm que se puede instalar en un clúster de {{site.data.keyword.cloud_notm}} Private local. Después de instalar el diagrama de Helm, encontrará {{site.data.keyword.blockchainfull_notm}} Platform como una plataforma en el catálogo de {{site.data.keyword.cloud_notm}} Private.

- {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se proporciona a través de Passport Advantage. Debe tener la licencia necesaria para acceder a [Passport Advantage Online](https://www.ibm.com/software/passportadvantage/pao_customer.html). Al realizar la compra, se incluye soporte técnico para la plataforma {{site.data.keyword.blockchainfull_notm}}.

- La edición Community Edition de {{site.data.keyword.blockchainfull_notm}} Platform está pensada para fines de exploración, desarrollo y pruebas. Se puede acceder a la versión gratuita de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private a través de GitHub. **Nota:** {{site.data.keyword.blockchainfull_notm}} Platform no proporciona soporte para Community Edition.

Para obtener instrucciones sobre cómo instalar el diagrama de Helm y los requisitos previos necesarios, consulte [Instalación de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/helm_install_icp.html#helm-install).

Si es un usuario nuevo de {{site.data.keyword.cloud_notm}} Private y desea información y sugerencias sobre cómo instalar y desplegar {{site.data.keyword.cloud_notm}} Private, consulte [Configuración de {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/ICP_setup.html#icp-setup).

Después de instalar {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private,
deberá desplegar cada componente de la red individualmente. No puede desplegar varios componentes al mismo tiempo. Consulte
[Iniciación a {site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/ibp_for_icp_deployment_guide.html#get-started-icp) para conocer los métodos recomendados para crear o unirse a una red blockchain. A continuación, revise los pasos para desplegar y trabajar con los componentes individuales en las secciones siguientes.

### Instalación de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private detrás de un cortafuegos
{: #ibp-icp-about-firewall}

Puede desplegar los componentes de {{site.data.keyword.blockchainfull_notm}} Platform detrás de un cortafuegos, sin tener que acceder a Internet público. El paquete del diagrama de Helm descargado incluye todas las imágenes de Docker de los componentes de Fabric que utiliza la plataforma {{site.data.keyword.blockchainfull_notm}}, sin obtenerlos de DockerHub durante el despliegue.

El paquete del diagrama de Helm de la edición Community Edition de {{site.data.keyword.blockchainfull_notm}} Platform no incluye las imágenes de Docker de los componentes de Fabric necesarios. Está configurado para descargar dichas imágenes desde DockerHub durante el despliegue y fallará si no tiene acceso a Internet público. No obstante, puede realizar algunos pasos adicionales para desplegar los componentes de Community Edition detrás de un cortafuegos. Para obtener más información, consulte, consulte
[Instalación de Community Edition detrás de un cortafuegos](/docs/services/blockchain/howto/helm_install_icp.html#helm-install-prereqs-firewall).


## Acerca de las entidades emisoras de certificados en {{site.data.keyword.cloud_notm}} Private
{: #ibp-icp-about-ca}

Las entidades emisoras de certificados (CA) proporcionan la identidad en la red. Una CA se puede considerar similar a un notario que actúa como punto de confianza entre varias partes. A todas las entidades de la red se les proporciona un certificado firmado por una CA raíz que encapsula su identidad digital. Este certificado es la raíz de la confianza para todas las operaciones de firma y verificación que se realizan en la red. Para obtener más información sobre las entidades emisoras de certificados y el rol que desempeñan en una red blockchain, consulte [Visión general de componentes de Blockchain](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview).

La CA validará la identidad y emitirá certificados para los demás componentes de la red que necesite desplegar. Como consecuencia, debe desplegar una CA para la organización antes de desplegar los demás componentes.

- Para aprender a configurar y a desplegar una CA después de instalar el diagrama de Helm, consulte [Despliegue de una entidad emisora de certificados en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/CA_deploy_icp.html#ca-deploy).

- Para obtener información sobre cómo utilizar la CA para generar certificados y completar los pasos de requisito previo para desplegar componentes adicionales, consulte [Funcionamiento de una entidad emisora de certificados en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/CA_operate.html#ca-operate).

## Acerca de los clasificadores en {{site.data.keyword.cloud_notm}} Private
{: #ibp-icp-about-orderer}

Los clasificadores autentican clientes, ordenan transacciones y difunden transacciones en una red blockchain. Constituyen el enlace común de las redes blockchain basadas en Hyperledger Fabric. Como consecuencia, la organización que crea una red debe desplegar e iniciar un "servicio de ordenación" (el nodo o recopilación de nodos que realizan la ordenación) para que las demás organizaciones puedan desplegar sus iguales, unirse a canales e iniciar transacciones en la red. Para obtener más información sobre los clasificadores y el rol que desempeñan en una red blockchain, consulte [Visión general de componentes de Blockchain](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview-orderer).

Si va a crear una red blockchain, necesitará desplegar un clasificador. Una vez que se haya desplegado, puede invitar a otras organizaciones a su consorcio, que luego podrán crear canales propios.

- Para ver cómo se configura y se despliega un clasificador después de instalar el diagrama de Helm, consulte [Despliegue de un clasificador en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/orderer_deploy_icp.html#icp-orderer-deploy).

- Para aprender a construir un consorcio, consulte [Funcionamiento de un clasificador en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/orderer_operate.html#icp-orderer-operate).

## Acerca de los iguales en {{site.data.keyword.cloud_notm}} Private
{: #ibp-icp-about-peer}

Los iguales son un elemento fundamental de la red, ya que alojan libros mayores y contratos inteligentes. Los contratos inteligentes y los libros mayores se utilizan para encapsular los procesos compartidos y la información compartida en una red, respectivamente. Para obtener más información sobre los iguales y el rol que desempeñan en una red blockchain, consulte [Visión general de componentes de Blockchain](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview).

- Cuando esté listo para unirse a una red, puede desplegar un igual que se unirá a canales, aprobará transacciones y almacenará los libros mayores del canal. Para obtener información sobre cómo desplegar un igual en {{site.data.keyword.cloud_notm}} Private que se conectará a otros componentes de {{site.data.keyword.cloud_notm}} Private, consulte [Despliegue de un igual en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/peer_deploy_icp.html#icp-peer-deploy). Para obtener información sobre cómo desplegar un igual en {{site.data.keyword.cloud_notm}} Private que se conectará a una red de Plan inicial o Plan empresarial, consulte [Despliegue de un igual que se conectará al Plan inicial o empresarial](/docs/services/blockchain/howto/peer_deploy_ibp.html#ibp-peer-deploy).

- Después de configurar el igual, deberá realizar varios pasos operativos para poder enviar transacciones y leer el libro mayor distribuido de la red blockchain.

  - Si va a conectar el igual a una {{site.data.keyword.blockchainfull_notm}} Platform desplegada en {{site.data.keyword.cloud_notm}} Private, consulte [Funcionamiento de iguales en {{site.data.keyword.cloud_notm}} privado con una red multinube](/docs/services/blockchain/howto/peer_operate_icp.html#icp-peer-operate).
  - Si va a conectar el igual a una red de Plan inicial o Plan empresarial desplegada en {{site.data.keyword.cloud_notm}}, consulte [Funcionamiento de iguales en {{site.data.keyword.cloud_notm}} Private con el Plan inicial o el Plan empresarial](/docs/services/blockchain/howto/peer_operate_ibp.html#ibp-peer-operate).

## Consideraciones sobre seguridad
{: #ibp-icp-about-security}

Debido a que estos componentes se despliegan fuera de {{site.data.keyword.cloud_notm}}, tendrá la responsabilidad de gestionar su seguridad. Esto incluye áreas importantes de seguridad, como la gestión de claves y el cifrado de datos. Examine los temas siguientes cuando tenga en cuenta la seguridad para los componentes.

### Seguridad de datos
{: #ibp-icp-about-security-data}

Los planes inicial y empresarial de {{site.data.keyword.blockchainfull_notm}} Platform utilizan el cifrado de disco completo que se basa en el [cifrado de claves simétricas ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SSB23S_1.1.0.14/gtps7/s7symm.html "Cifrado simétrico") para proteger todos los datos que utilizan las redes. Debe seguir pasos similares en su propio entorno para proteger los datos de los iguales.

Los datos de la base de datos de estado, independientemente de si utiliza LevelDB o CouchDB, no se cifran. Puede utilizar un cifrado a nivel de aplicación para proteger los datos en reposo en la base de datos de estado.

### Residencia de datos
{: #ibp-icp-about-security-data-residency}

Los requisitos de residencia de datos pueden imponer que el proceso y el almacenamiento de todos los datos del libro mayor de blockchain permanezcan dentro de los límites de un solo país (o dentro de algún otro límite definido). Para obtener más información sobre cómo conseguir la residencia de datos, consulte [Residencia de los datos](#ibp-icp-about-data-residency).

### Gestión de claves
{: #ibp-icp-about-security-key-management}

La gestión de claves es un aspecto crítico de la seguridad. Si una clave privada se ve comprometida o se pierde, es posible que usuarios hostiles accedan a los datos y funciones. IBM utiliza dispositivos físicos conocidos como [Módulos de seguridad de hardware](/docs/services/blockchain/glossary.html#glossary-hsm) (HSM) para almacenar las claves privadas de las redes del Plan empresarial de la plataforma {{site.data.keyword.blockchainfull_notm}}.

Cuando despliegue un componente en {{site.data.keyword.cloud_notm}} Private, usted es el responsable de gestionar las claves privadas. Aunque {{site.data.keyword.blockchainfull_notm}} Platform genera claves privadas, dichas claves no se almacenan en la plataforma. Es de vital importancia que almacene sus claves de forma segura para que no se vean comprometidas. Encontrará la clave privada del componente en la carpeta de almacén de claves de MSP del igual, en el directorio `/mnt/crypto/peer/peer/msp/keystore/` dentro del componente. Para obtener más información sobre los certificados que hay dentro de su igual, consulte la sección [Proveedor de servicios de pertenencia](/docs/services/blockchain/certificates.html#managing-certificates-msp) de la guía de aprendizaje sobre [Gestión de certificados en {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain/certificates.html#managing-certificates).

Puede utilizar Key Escrow para recuperar claves privadas perdidas. Esto hay que hacerlo antes de perder ninguna clave. Si una clave privada no se puede recuperar, tiene que obtener nuevas claves privadas registrando una nueva identidad con la entidad emisora de certificados. También debe eliminar y sustituir signCert de cualquier canal al que se haya unido.

### TLS
{: #ibp-icp-about-security-tls}

[La seguridad de capa de transporte ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10660_.htm "Una visión general del reconocimiento SSL o TLS") (TLS) está integrada en el modelo de confianza de Hyperledger Fabric. Todos los componentes del Plan inicial o empresarial de {{site.data.keyword.blockchainfull_notm}} Platform utilizan TLS para autenticarse y comunicarse entre sí. Por lo tanto, los componentes de red de la plataforma deben ser capaces de completar un reconocimiento de TLS con sus iguales. Una implicación de este enfoque es que necesita activar el paso a través, usando por ejemplo una lista blanca, en el cortafuegos de las apps cliente a su igual.

### Configuración del proveedor de servicios de pertenencia
{: #ibp-icp-about-security-MSP}

Los componentes de {{site.data.keyword.blockchainfull_notm}} Platform consumen identidades a través de proveedores de servicios de pertenencia (MSP). Los MSP asocian los certificados que emiten las entidades emisoras de certificados con roles de red y de canal. Para obtener más información sobre cómo funcionan los MSP con el igual, consulte [Proveedores de servicios de pertenencia (MSP)](/docs/services/blockchain/certificates.html#managing-certificates-msp).

### Seguridad de las aplicaciones
{: #ibp-icp-about-security-appl}

Puesto que todas las invocaciones de código de encadenamiento están firmadas, Fabric gestiona la seguridad de las aplicaciones. Además, Fabric también incluye comprobaciones de nivel de aplicación basadas en ACL.

## Residencia de datos
{: #ibp-icp-about-data-residency}

Debido a que las redes blockchain no conocen qué tipo de datos se procesa, en ocasiones deben realizarse pasos adicionales para mantener seguros determinados tipos de datos. El requisito más común en cuanto a residencia de datos está asociado a las leyes de determinados países, según las cuales todos los datos que se procesan y almacenan en un sistema de TI deben permanecer dentro de las fronteras del país específico. Paralelamente, algunas empresas de sectores muy regulados, como las gubernamentales, de sanidad y de servicios financieros, obligan a que los datos se almacenen tras su cortafuegos. Por lo tanto, para conseguir la residencia de datos, todos los componentes de la red blockchain deben formar parte del mismo [canal](/docs/services/blockchain/glossary.html#glossary-channel) y deben residen dentro de las fronteras de un solo país.

Para hacer frente a los requisitos de residencia de datos, es importante comprender la arquitectura de Hyperledger Fabric subyacente a la plataforma {{site.data.keyword.blockchainfull_notm}}. La arquitectura se centra en torno a tres componentes clave: un servicio de ordenación (compuesto por clasificadores), entidades emisoras de certificados (CA) e iguales. Un igual recibe actualizaciones de estado ordenadas en forma de bloques desde el servicio de ordenación y mantiene el estado y el libro mayor. Por lo tanto, un igual y un servicio de ordenación tienen una relación directa. El libro mayor contiene los valores más recientes de todas las claves y los datos que incluyen los registros de transacciones.

Además, las aplicaciones cliente utilizan los [SDK de Fabric](/docs/services/blockchain/v10_application.html#dev-app-fabric-sdks) para enviar transacciones a los iguales y al servicio de ordenación. Estas transacciones incluyen datos del [conjunto de lectura-escritura ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/readwrite.html "semántica del conjunto de lectura-escritura"), que contienen los valores de clave-valor en el libro mayor.

Si la residencia de datos en el país es un requisito, el clasificador, el igual y las aplicaciones cliente deben residir en el mismo país. Cuando se crea una red de {{site.data.keyword.blockchainfull_notm}} Platform en {{site.data.keyword.cloud_notm}}, tiene la opción de seleccionar la ubicación de la red. <!--For a Starter Plan network, you can select from US South, United Kingdom, and Sydney. For an Enterprise Plan network, you can select from currently available locations, which include Dallas, Frankfurt, London, Sao Paulo, Tokyo, and Toronto. -->Para obtener más información sobre regiones y ubicaciones, consulte el tema sobre [Regiones y ubicaciones de {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain/reference/ibp_regions.html#ibp-regions-locations).

### Un caso de uso para la residencia de datos

Tenga en cuenta una red de {{site.data.keyword.blockchainfull_notm}} Platform que incluye el clasificador y la entidad emisora de certificados junto con un consorcio de cuatro organizaciones. Las organizaciones tienen uno o más nodos de igual, las cuatro organizaciones forman parte de un único canal y todos los componentes de la red se encuentran en la región (por ejemplo, Frankfurt) donde se ha desplegado la red de la plataforma {{site.data.keyword.blockchainfull_notm}}. Por último, las aplicaciones cliente que interactúan con los iguales también residen en Alemania.

En este ejemplo, se mantiene la residencia de datos.

![Residencia de datos cuando todos los componentes se encuentran en el mismo país](images/remote_peer_data_res_1.png "Residencia de datos cuando todos los componentes se encuentran en el mismo país")
*Figura 1. Residencia de datos cuando todos los componentes se encuentran en el mismo país*

Ahora, tengamos en cuenta las implicaciones de que un **igual distribuido** se una a una de las organizaciones. Un igual distribuido puede residir en la misma región que el resto de la red o en cualquier lugar fuera de la región de la red de la plataforma
{{site.data.keyword.blockchainfull_notm}}:

-	Si el igual reside en el mismo país que el resto de la red, se mantiene la residencia de datos. Todos los datos del libro mayor permanecen dentro de Alemania, como indica la **Figura 1** anterior.
-	En caso de que el igual resida en un país distinto (como EE. UU. por ejemplo), ya no se mantiene la residencia de datos, pues los datos del libro mayor del igual se comparten fuera de la frontera del país.

Para resolver este problema, se pueden utilizar **canales** para aislar los datos en un subconjunto de iguales de la red. Cuando la red de {{site.data.keyword.blockchainfull_notm}} Platform contiene un igual distribuido y clasificadores entre fronteras, los canales proporcionan el aislamiento de los datos de libro mayor de organizaciones que tienen iguales fuera de la frontera del país.

**Nota:** las clasificadores siempre están ubicados en la región del centro de datos que haya seleccionado para alojar la red. No es posible tener varios clasificadores entre países. Sin embargo, los iguales pueden estar ubicados en el centro de datos o en una ubicación remota fuera de {{site.data.keyword.cloud_notm}}.

![Residencia de los datos cuando los iguales están fuera del país de la región de {{site.data.keyword.blockchainfull_notm}} Platform](images/remote_peer_data_res_2.png "Residencia de los datos cuando los iguales están fuera del país de la región de {{site.data.keyword.blockchainfull_notm}} Platform")
*Figura 2. Residencia de los datos cuando los iguales están fuera del país de la región de {{site.data.keyword.blockchainfull_notm}} Platform*

En la **Figura 2**, no se requiere residencia de datos para `OrgC` y `OrgD`. De hecho,
`OrgD` incluye ahora dos iguales distribuidos, `OrgD-peer1` y `OrgD-peer2`, que residen en *Estados Unidos*. Por lo tanto, para que `OrgA`, `OrgB` y sus respectivas aplicaciones cliente e iguales que residen en Alemania puedan aislar los datos de libro mayor en el canal `X`, se crea un nuevo canal `Y` para
`OrgC` y `OrgD`.

Para estudiar con mayor detalle el flujo de datos en la red de la plataforma
{{site.data.keyword.blockchainfull_notm}}, consulte la
[documentación de Fabric sobre el flujo de transacciones
![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/txflow.html "Flujo de transacciones").

En el futuro, la nueva tecnología de Hyperledger Fabric mejorará la capacidad de obtener una mejor residencia de datos utilizando [Recopilaciones de datos privados ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data/private-data.html "Recopilaciones de datos privados") y Zero Knowledge Proof.

- Una recopilación de datos privados garantiza que los datos privados se comparten entre igual e igual (mediante el protocolo gossip) solo con los iguales que tienen autorización para verlos, por ejemplo iguales que están dentro de las fronteras del país. Los datos se almacenan en una base de datos privada en el igual. El servicio de ordenación no está implicado y no ve los datos privados. Se escribe un hash de esos datos en los libros mayores de cada igual del canal. El hash que se utiliza para la validación de estado sirve como prueba de la transacción y se puede utilizar para fines de auditoría. Los datos privados están disponibles para las redes de {{site.data.keyword.blockchainfull_notm}} Platform que se ejecutan en la versión 1.2.1 o superior de Fabric. No obstante, la característica de datos privados no está disponible para los iguales que se ejecutan en {{site.data.keyword.cloud_notm}} Private, ya que las redes de {{site.data.keyword.cloud_notm}} Private no utilizan gossip (rumores) actualmente.

- Una ZKP (zero knowledge proof) permite que un "comprobador" asegure a un "verificador" que conoce un secreto sin tener que revelar el propio secreto.

Puede obtener más información sobre estas tecnologías en el documento técnico sobre [Transacciones privadas y confidenciales con Hyperledger Fabric ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://developer.ibm.com/tutorials/cl-blockchain-private-confidential-transactions-hyperledger-fabric-zero-knowledge-proof/ "Transacciones privadas y confidenciales con Hyperledger Fabric").

## Obtención de soporte
{: #ibp-icp-about-support}

Para obtener más información sobre las ofertas de soporte digital, consulte los [Recursos y foros de soporte](/docs/services/blockchain/ibmblockchain_support.html#blockchain-support-resources) de {{site.data.keyword.blockchainfull_notm}} Platform.

### {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private

Si ha adquirido una licencia de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private y desea ponerse en contacto con el equipo de atención al cliente, consulte la información sobre [acceso a IBM Support Community y apertura de una incidencia de soporte ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://www-01.ibm.com/support/docview.wss?uid=ibm10740041 "Soporte de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private").

### Community Edition de la plataforma {{site.data.keyword.blockchainfull_notm}}

La edición Community Edition está pensada para exploración, desarrollo y pruebas. {{site.data.keyword.blockchainfull_notm}} Platform no proporciona soporte para la edición Community Edition de la plataforma {{site.data.keyword.blockchainfull_notm}}.

Si detecta algún problema relacionado con los componentes de blockchain, puede utilizar los recursos gratuitos de desarrollador de blockchain y los foros de soporte para obtener ayuda de la comunidad de Fabric y de IBM. Para obtener más información, consulte [Recursos de blockchain y foros de soporte](/docs/services/blockchain/ibmblockchain_support.html#blockchain-support-resources).

Para los problemas relacionados con IBM Cloud privado, puede aprovechar el
[soporte digital gratuito y el soporte de pago que ofrece {{site.data.keyword.cloud_notm}} Private](https://www.ibm.com/developerworks/community/blogs/fe25b4ef-ea6a-4d86-a629-6f87ccf4649e/entry/Learn_more_about_IBM_Cloud_Private_Support?lang=en_us).
