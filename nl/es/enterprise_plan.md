---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-16"

keywords: blockchain network, Enterprise Plan, production-ready network

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca del Plan empresarial
{: #enterprise-plan-about}

El Plan empresarial de {{site.data.keyword.blockchainfull}} Platform es una oferta lista para producción disponible para las organizaciones que quieran crear una red empresarial blockchain o unirse a una. Este plan proporciona la infraestructura clave junto con las herramientas y el soporte necesarios para iniciar con facilidad una red muy segura y lista para producción. El Plan empresarial se ha actualizado de Hyperledger Fabric V1.0 a V1.1 el 15 de mayo de 2018. Todas las redes creadas después del 15 de mayo de 2018 están en el nivel de Fabric V1.1. Sin embargo, las redes creadas anteriormente permanecerán en el nivel V1.0 de fábrica.
{:shortdesc}

El **Plan empresarial** es un entorno de producción que ofrece altos niveles de seguridad y soporte. El despliegue de la red en el Plan empresarial le permite aprovechar las características siguientes:

* Un entorno altamente seguro con muchas características de seguridad de software, firmware y hardware.
* Arquitectura reforzada para la escalabilidad, la capacidad de recuperación y la disponibilidad.
* Optimización del rendimiento y la ejecución en el sistema Linux más rápido del mundo.

El funcionamiento de la red en {{site.data.keyword.blockchainfull_notm}} Platform incluye herramientas y prestaciones que facilitan las tareas administrativas:

* Paneles de control para la supervisión y gestión de los recursos de la red.
* Actualizaciones sencillas de la pila de código completa.
* Soporte técnico 24/7 integrado en el portal.
* Pila de seguridad reforzada sin acceso privilegiado, malware y a prueba de manipulación, cifrada completamente y con muchas más características para redes con datos sensibles en los sectores regulados.
* Se realiza una copia de seguridad externa de las redes de empresa cada 24 horas. En el caso de que se produzca un desastre, estas redes se pueden restaurar en el mismo sitio o en un sitio alternativo.

**Notas:**
- El Plan empresarial proporciona un entorno de producción. Si necesita un entorno de desarrollo y pruebas, consulte [Acerca del Plan inicial](/docs/services/blockchain/starter_plan.html#starter-plan-about).
- {{site.data.keyword.blockchainfull_notm}} Platform es un servicio de plataforma de {{site.data.keyword.cloud_notm}} y todas las ofertas de pertenencia a grupo siguen las [condiciones de los servicios de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm "condiciones de servicios de {{site.data.keyword.cloud_notm}}") de los acuerdos de nivel de servicio (SLA). Las redes del Plan empresarial se proporcionan en un centro de datos de una única ubicación geográfica. Para ver una lista de los lugares geográficos disponibles, consulte
[Ubicaciones de {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain?topic=blockchain-ibp-regions-locations#ibp-regions-locations).

Para los miembros que van a iniciar la red, IBM proporciona una interfaz gráfica de usuario para guiar al iniciador de la red a través de los pasos clave para establecer y suministrar la red. Ello incluye invitar a otros miembros y definir las reglas de gobierno. Para obtener más información, consulte [Gobierno de la red del Plan empresarial](/docs/services/blockchain/get_start.html#getting-started-with-enterprise-plan). Una vez desplegada la red, dispondrá de una interfaz gráfica de usuario, el supervisor de red, para supervisar la actividad y el estado de la red, gestionar las actividades de red clave (que incluyen nuevos despliegues, adición o eliminación de miembros, ciclo de vida del código de encadenamiento y gestión de canales) y buscar soporte técnico. Para obtener más información, consulte [Utilización del supervisor de red](/docs/services/blockchain/v10_dashboard.html#ibp-dashboard).

Regístrese ahora para pertenecer al grupo de [{{site.data.keyword.blockchainfull_notm}} ![Icono de enlace externo](images/external_link.svg "Icono de enlace externo")](https://cloud.ibm.com/catalog/services/ibm-blockchain-5-prod).

{{site.data.keyword.blockchainfull_notm}} Platform se crea con componentes clave de Hyperledger Fabric, que incluyen una entidad emisora de certificados (CA) y al menos 1 igual (con un máximo de 6).  El Plan empresarial también proporciona un servicio de ordenación Kafka tolerante a errores de caída (CFT) para los miembros de la red.

La CA de Fabric es la entidad emisora de certificados que se proporciona con el Plan empresarial. Se suministran dos CA intermedias por miembro, que otorgan pertenencia a la red. Mediante la CA, el miembro también puede proporcionar certificados de pertenencia a los usuarios de la red.

Es importante comprender que en el proceso de adición de una transacción al libro mayor intervienen tres fases:
1. Simulación de transacción y aprobación (igual)
2. Ordenación (servicio de ordenación)
3. Validación y confirmación (igual)

Los iguales de Fabric propiedad de los miembros son la interfaz o pasarela para las aplicaciones que ejecutan el código de encadenamiento y, con ello, proporcionan la lógica empresarial para la ejecución de transacciones del libro mayor. Deben aprobarse todas las transacciones. Los otros miembros de la red llevan a cabo esta aprobación. Tras la aprobación, las transacciones se envían a un servicio de ordenación de IBM.

Además de los componentes principales de blockchain, la opción de pertenencia Empresarial proporciona una infraestructura con almacenamiento de datos y comunicaciones seguras (TLS) así como alta disponibilidad.  Aunque las redes de Fabric comparten estos recursos de infraestructura, se proporciona aislamiento en los nodos de los componentes de Fabric de una red y cada nodo se ejecuta en un contenedor de Docker seguro que protege el entorno de ejecución.

El único aspecto que se debe determinar es el tamaño de los iguales que necesita la red. Esta decisión se basa en el número de canales necesarios, además de la carga por canal, el uso de memoria y el espacio en disco (almacenamiento).

Debe utilizar el Plan empresarial para despliegues más estables, de producción o casi de nivel de producción. A efectos de prueba, utilice el [Plan inicial](/docs/services/blockchain/starter_plan.html#starter-plan-about) o [instale imágenes de Docker localmente](https://hyperledger-fabric.readthedocs.io/en/release-1.2/build_network.html).

<!--- The Enterprise plan provides the ordering service and CA. The membership fee is $1,000, and a per peer fee of $1,000 that is associated with the network. If you want to have high availability (HA), you must purchase an additional peer to provide the HA capabilities. For example, one organization (associated membership fee of $1,000) of two peers ($1,000 X 2 peers) with HA ($1,000 X 2 HA peers) requires a monthly charge of $5,000.  --->

## Precios
{: #enterprise-plan-about-pricing}

Para utilizar el Plan empresarial, los miembros de la red deben pagar 1.000 $ al mes como cuota de suscripción y otros 1.000 $ al mes por cada uno de los iguales de la red.  Las cuotas mensuales se facturan prorrateadas por día.  Por ejemplo, un miembro (cuota de suscripción asociada de 1.000 $) con dos iguales (la cuota por igual es de 1.000 $ X 2 iguales) pagaría 3.000 $ al mes.  Si el mes tiene 30 días, el miembro paga 100 $ (3.000 $/30) al día.  Tenga en cuenta que, si necesita alta disponibilidad (HA), debe doblar el número de iguales necesarios para disponer de las funciones de HA.

Los miembros de la red pueden abonar su factura con sus propias cuentas de {{site.data.keyword.cloud_notm}} que contienen el espacio para crear la instancia de la red. Si lo desea, un miembro de la red puede hacerse cargo de la factura de todos los miembros de la red. Para obtener más información sobre cómo abonar las redes blockchain, consulte el apartado [Pago de la red](/docs/services/blockchain/howto/paying_mode.html#paying-mode).
