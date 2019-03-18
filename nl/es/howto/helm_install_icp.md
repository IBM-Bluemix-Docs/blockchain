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
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}

# Instalación de {{site.data.keyword.blockchainfull_notm}} Platform en {{site.data.keyword.cloud_notm}} Private
{: #helm-install}

{{site.data.keyword.blockchainfull}} Platform para {{site.data.keyword.cloud_notm}} Private se entrega como un archivo de diagrama de Helm que se puede instalar en un clúster de {{site.data.keyword.cloud_notm}} Private local. Después de instalar el diagrama de Helm, encontrará {{site.data.keyword.blockchainfull_notm}} Platform como una plataforma en el catálogo de {{site.data.keyword.cloud_notm}} Private.

Antes de instalar {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private, revise las
[Consideraciones y limitaciones](/docs/services/blockchain/ibp-for-icp-about.html#ibp-icp-about-considerations). Para obtener más información sobre cómo desplegar los componentes de blockchain que se incluyen en el diagrama de Helm, los precios y el soporte, consulte
[Acerca de {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/ibp-for-icp-about.html#ibp-icp-about).

{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private ofrece dos ediciones:

- {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private se proporciona a través de Passport Advantage (PPA). Debe tener la licencia necesaria para acceder a
[Passport Advantage Online ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/software/passportadvantage/pao_customer.html "Passport Advantage Online"). Al realizar la compra, se incluye soporte técnico para la plataforma {{site.data.keyword.blockchainfull_notm}}.

- La edición Community Edition de {{site.data.keyword.blockchainfull_notm}} Platform es una oferta gratuita para exploración, desarrollo y pruebas. Es posible acceder a esta versión gratuita a través de
[GitHub ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/IBM/charts/tree/master/stable/ibm-blockchain-platform-dev "IBM/charts"). Tenga en cuenta que
{{site.data.keyword.IBM_notm}} no proporciona soporte para Community Edition.

## Requisitos previos para la instalación del diagrama de Helm
{: #helm-install-prereqs}

Antes de instalar el diagrama de Helm, debe haber configurado un clúster de {{site.data.keyword.cloud_notm}} Private. Consulte las instrucciones para
[configurar un clúster de {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/ICP_setup.html#icp-setup).

## Instalación de {{site.data.keyword.blockchainfull_notm}} Platform detrás de un cortafuegos
{: #helm-install-prereqs-firewall}

Puede desplegar componentes de {{site.data.keyword.blockchainfull_notm}} Platform detrás de un cortafuegos sin conectividad de
Internet. El paquete PPA incluye todas las imágenes de Docker de componentes de Fabric que utilizará la plataforma
{{site.data.keyword.blockchainfull_notm}}, por lo que no necesita descargarlas de DockerHub durante el despliegue.

No obstante, el diagrama de Helm de Community Edition no incluye las imágenes de Docker de componentes de Fabric necesarias, ya que esta edición está configurada para descargar dichas imágenes de DockerHub durante el despliegue. El despliegue fallará si no hay conexión a Internet. Por lo tanto, debe realizar pasos adicionales para crear archivados en una máquina conectada a Internet para poder instalar los archivados en el clúster de {{site.data.keyword.cloud_notm}} Private. Las imágenes siguientes son necesarias:
- [Igual de Fabric
![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hub.docker.com/r/ibmcom/ibp-fabric-peer/ "Igual de Fabric")
- [CA de Fabric
![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hub.docker.com/r/ibmcom/ibp-fabric-ca/ "CA de Fabric")
- [Clasificador de Fabric
![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hub.docker.com/r/ibmcom/ibp-fabric-orderer/ "Clasificador de Fabric")
- [Base de datos de Couch de Fabric ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hub.docker.com/r/ibmcom/ibp-fabric-couchdb/ "Base de datos de Couch de Fabric")
- Imagen [`Init` utilizada para arrancar y configurar componentes, incluyendo las carpetas de MSP ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hub.docker.com/r/ibmcom/ibp-init/)
- [Imagen Docker-in-Docker (DinD) utilizada por los iguales para ejecutar contenedores de código de encadenamiento ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hub.docker.com/r/ibmcom/ibp-dind/)

Para obtener más información sobre cómo utilizar estas imágenes, consulte
[Adición de aplicaciones destacadas a clústeres sin conexión a Internet ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.0/app_center/add_package_offline.html). Tenga en cuenta que puede encontrar el archivo de especificación `manifest.yaml` en el directorio
`ibm-blockchain-platform-dev/ibm_cloud_pak` del diagrama de Helm.

## Importación del diagrama de Helm en {{site.data.keyword.cloud_notm}} Private

1. Descargue el archivo del diagrama de Helm en IBM Blockchain Platform para {{site.data.keyword.cloud_notm}} Private desde [Passport Advantage Online ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://www.ibm.com/software/passportadvantage/pao_customer.html "Passport Advantage Online") o para la edición gratuita Community desde [GitHub ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/IBM/charts/blob/master/repo/stable/ibm-blockchain-platform-dev-1.0.0.tgz "IBM/charts").  Este paquete de diagramas de Helm contiene tres subdiagramas de Helm para la CA, el clasificador y el igual.

2. Si aún no lo ha hecho, inicie sesión en el clúster de {{site.data.keyword.cloud_notm}} Private.

  ```
  cloudctl login -a https://<cluster_CA_domain>:8443 --skip-ssl-validation
  ```
  {:codeblock}

4. Asegúrese de configurar la [CLI de Docker](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.0/manage_images/configuring_docker_cli.html). Tras configurar la CLI de Docker, acceda al registro de imágenes del clúster utilizando el mandato siguiente:
  ```
  docker login <cluster_CA_domain>:8500
  ```
  {:codeblock}

5. Busque el nombre del repositorio en {{site.data.keyword.cloud_notm}} Private para cargar el diagrama de Helm utilizando el mandato siguiente:
  ```
  cloudctl catalog repos
  ```
  {:codeblock}

  Cuando este mandato finalice correctamente, podrá ver una lista de repositorios del clúster. Elija el nombre del repositorio de destino y guárdelo. Necesitará utilizarlo en el mandato siguiente.

6. Importe el diagrama de Helm utilizando la línea de mandatos.
  El mandato que ejecute para importar el diagrama de Helm dependerá de si el diagrama de Helm se ha descargado de Passport Advantage (PPA) o de GitHub.

  - **{{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private**

    Siga estas instrucciones si ha descargado el diagrama de Helm de PPA.
    Desde el directorio en el que ha almacenado el diagrama de Helm descargado de PPA, ejecute el mandato siguiente en la CLI de {{site.data.keyword.cloud_notm}} Private para importar el diagrama de Helm en el clúster de {{site.data.keyword.cloud_notm}} Private.

    ```
    cloudctl catalog load-archive --archive <archive-name> --registry <cluster_CA_domain>:8500 --repo <repo-name>
    ```
    {:codeblock}

    Sustituya los valores siguientes:
    - `<archive-name>` por el nombre del archivo `.tgz` descargado.
    - `<cluster_CA_domain>:8500` por el dominio que utilice para iniciar sesión en el clúster de {{site.data.keyword.cloud_notm}} Private.
    - `<repo-name>` por el repositorio de Helm donde desee cargar el diagrama. Ejecute 'cloudctl catalog repos' para ver una lista de los repositorios.

    Cuando este mandato finalice correctamente, verá algo parecido a la información siguiente:

    <details aria-label="Details"><summary>Helm install output</summary>
    ```
    Expanding archive
    OK

    Importing docker images
      Processing image: ibmblockchain/hlfabric-orderer-amd64:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-orderer-amd64:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-orderer-amd64:1.2.1
      Processing image: ibmblockchain/hlfabric-orderer-s390x:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-orderer-s390x:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-orderer-s390x:1.2.1
      Processing image: ibmblockchain/hlfabric-ca-amd64:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-ca-amd64:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-ca-amd64:1.2.1
      Processing image: ibmblockchain/hlfabric-ca-s390x:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-ca-s390x:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/hlfabric-ca-s390x:1.2.1
      Processing image: ibmblockchain/v1fabric-peer-amd64:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/v1fabric-peer-amd64:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/v1fabric-peer-amd64:1.2.1
      Processing image: ibmblockchain/v1fabric-peer-s390x:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/v1fabric-peer-s390x:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/v1fabric-peer-s390x:1.2.1
      Processing image: ibmblockchain/fabric-couchdb-amd64:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/fabric-couchdb-amd64:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/fabric-couchdb-amd64:1.2.1
      Processing image: ibmblockchain/fabric-couchdb-s390x:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmblockchain/fabric-couchdb-s390x:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmblockchain/fabric-couchdb-s390x:1.2.1
      Processing image: ibmcom/icp-dind-amd64:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmcom/icp-dind-amd64:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmcom/icp-dind-amd64:1.2.1
      Processing image: ibmcom/icp-dind-s390x:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmcom/icp-dind-s390x:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmcom/icp-dind-s390x:1.2.1
      Processing image: ibmcom/icp-busybox-s390x:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmcom/icp-busybox-s390x:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmcom/icp-busybox-s390x:1.2.1
      Processing image: ibmcom/icp-busybox-amd64:1.2.1
      Loading Image
      Tagging Image
      Pushing image as: mycluster.icp:8500/bcaas-usa/ibmcom/icp-busybox-amd64:1.2.1
    Pushing image mycluster.icp:8500/bcaas-usa/ibmcom/icp-busybox-amd64:1.2.1
    OK

    Uploading helm charts
      Processing chart: charts/ibm-blockchain-platform-0.1.5.tgz
      Updating chart values.yaml
      Uploading chart
    Loaded helm chart
    OK

    Synch charts
  Synch started
  OK
    ```

  - **Community Edition descargada desde GitHub**
    Siga estas instrucciones si ha descargado el diagrama de Helm de GitHub.

    Desde el directorio en el que ha almacenado el diagrama de Helm descargado de GitHub, ejecute el mandato siguiente en la CLI de {{site.data.keyword.cloud_notm}} Private para importar el diagrama de Helm en el clúster de {{site.data.keyword.cloud_notm}} Private. Para importar el diagrama de Helm descargado de GitHub, ejecute el mandato siguiente:
    ```
    cloudctl catalog load-chart --archive <helm_chart_from_github> --repo <repo-name>
    ```
    {:codeblock}

    Sustituya los valores siguientes:
    - `<helm_chart_from_github>` por el nombre del archivo .tgz que ha descargado.
    - `<repo-name>` por el repositorio de Helm donde desee cargar el diagrama. Ejecute 'cloudctl catalog repos' para ver una lista de los repositorios.

    Cuando este mandato finalice correctamente, verá algo parecido a la información siguiente:
    ```
    Loading helm chart
  Loaded helm chart

    Synch charts
  Synch started
  OK
    ```

Pulse el botón **Catálogo** de la consola de {{site.data.keyword.cloud_notm}} Private y, a continuación, pulse **Blockchain** en el panel de navegación de la izquierda para verificar que la importación se ha realizado correctamente. Si es así, el mosaico **ibm-blockchain-platform-prod** o el mosaico **ibm-blockchain-platform-dev** debe estar visible en la página Catálogo de {{site.data.keyword.cloud_notm}} Private.


## Requisitos de PodSecurityPolicy

Tras importar el diagrama de Helm en {{site.data.keyword.cloud_notm}} Private, deberá enlazar una política
[PodSecurityPolicy
![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://kubernetes.io/docs/concepts/policy/pod-security-policy/ "Políticas de seguridad de pod") con el espacio de nombres de destino antes de instalar los componentes.  Elija una política de seguridad de pod (PodSecurityPolicy) predefinida o solicite al administrador del clúster que cree una PodSecurityPolicy personalizada:
- Nombre de PodSecurityPolicy predefinida: [`ibm-privileged-psp`](https://ibm.biz/cpkspec-psp)
- Nombre de PodSecurityPolicy personalizada:
  ```
  apiVersion: extensions/v1beta1
  kind: PodSecurityPolicy
  metadata:
    name: ibm-blockchain-platform-psp
  spec:
    hostIPC: false
    hostNetwork: false
    hostPID: false
    privileged: true
    allowPrivilegeEscalation: true
    readOnlyRootFilesystem: false
    seLinux:
      rule: RunAsAny
    supplementalGroups:
      rule: RunAsAny
    runAsUser:
      rule: RunAsAny
    fsGroup:
      rule: RunAsAny
    requiredDropCapabilities:
    - ALL
    allowedCapabilities:
    - NET_BIND_SERVICE
    - CHOWN
    - DAC_OVERRIDE
    - SETGID
    - SETUID
    volumes:
    - '*'
  ```
  {:codeblock}
- ClusterRole (rol de clúster) personalizado para la PodSecurityPolicy personalizada:
  ```
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    annotations:
    name: ibm-blockchain-platform-clusterrole
  rules:
  - apiGroups:
    - extensions
    resourceNames:
    - ibm-blockchain-platform-psp
    resources:
    - podsecuritypolicies
    verbs:
    - use
  - apiGroups:
    - ""
    resources:
    - secrets
    verbs:
    - create
    - delete
    - get
    - list
    - patch
    - update
    - watch
  ```
  {:codeblock}

- ClusterRoleBinding (enlace de rol de clúster) personalizado para el ClusterRole personalizado:
  ```
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRoleBinding
  metadata:
   name: ibm-blockchain-platform-clusterrolebinding
  roleRef:
   apiGroup: rbac.authorization.k8s.io
   kind: ClusterRole
   name: ibm-blockchain-platform-clusterrole
  subjects:
  - kind: ServiceAccount
    name: default
    namespace: default
  ```
  {:codeblock}

## Despliegue de componentes individuales

Después de instalar el diagrama de Helm, pulse el mosaico **ibm-blockchain-platform-prod** o **ibm-blockchain-platform-dev** en el catálogo de {{site.data.keyword.cloud_notm}} Private para abrirlo. Puede utilizar la página de configuración para desplegar cualquiera de los componentes individuales de la red blockchain. Para obtener más detalles sobre los componentes necesarios para la solución de blockchain y sobre el orden en el que deben desplegarse, consulte [Iniciación a {{site.data.keyword.blockchainfull_notm}} Platform para {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/ibp_for_icp_deployment_guide.html#get-started-icp).

A continuación, despliegue los componentes individuales:

- Si va a desplegar un clasificador, en primer lugar debe configurar una entidad emisora de certificados para el clasificador. La CA generará certificados que utilizarán los demás componentes de la organización. Para obtener más información, consulte [Despliegue de una entidad emisora de certificados de {{site.data.keyword.blockchainfull_notm}} Platform en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/CA_deploy_icp.html#ca-deploy). A continuación, puede desplegar el clasificador, que será el enlace común de la red. Para obtener más información, consulte [Despliegue de un clasificador de {{site.data.keyword.blockchainfull_notm}} Platform en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/orderer_deploy_icp.html#icp-orderer-deploy)

- Si va a desplegar un igual, en primer lugar debe configurar una entidad emisora de certificados para el igual. La CA generará los certificados que utilizará el igual. Para obtener más información, consulte [Despliegue de una entidad emisora de certificados de {{site.data.keyword.blockchainfull_notm}} Platform en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/CA_deploy_icp.html#ca-deploy). A continuación, cuando esté listo para unirse a una red, puede desplegar los iguales que se unirán a canales, aprobarán transacciones y almacenarán los datos. Para obtener más información, consulte [Despliegue de un igual de {{site.data.keyword.blockchainfull_notm}} en {{site.data.keyword.cloud_notm}} Private](/docs/services/blockchain/howto/peer_deploy_icp.html#icp-peer-deploy) o [Despliegue de un igual de {{site.data.keyword.blockchainfull_notm}} para una red de Plan inicial o Plan empresarial](/docs/services/blockchain/howto/peer_deploy_ibp.html#ibp-peer-deploy), dependiendo de la red blockchain a la que se vaya a unir el igual.
