---

copyright:
  years: 2018
lastupdated: "2018-06-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Despliegue de aplicaciones de ejemplo
{: #overview}

La plataforma {{site.data.keyword.blockchainfull}} proporciona aplicaciones de ejemplo que puede desplegar y probar, a fin de comprender mejor las redes de blockchain y el proceso de desarrollo de aplicaciones.
{: shortdesc}

|  Ejemplos     | Caso de uso       | Tipo de muestra  | Creador y soporte  |
| --------------|---------------------|----|-------|
| [Marbles ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/IBM-Blockchain/marbles)| Varios usuarios pueden crear canicas con diferentes propiedades y transferirlas a otros. <br> <br> Siga las instrucciones para desplegar Marbles en el servicio de {{site.data.keyword.blockchainfull_notm}} en {{site.data.keyword.cloud_notm}}. Tenga en cuenta que las capturas de pantalla muestran la IU del Plan empresarial, en lugar del Plan de iniciador. La funcionalidad es similar. | Código de encadenamiento de GO con una aplicación Javascript| IBM<br> [Obtener ayuda![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/IBM-Blockchain/marbles/issues) |
|[Fabricación de vehículos ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/IBM-Blockchain/vehicle-manufacture) | Los usuarios pueden pasar por el ciclo de vida de un vehículo virtual.  <br> <br> Siga las instrucciones para **Desplegar manualmente esta demostración en IBM Cloud** para obtener una guía paso a paso para desplegar el ejemplo en la red.| Definición de la red empresarial de [Hyperledger Composer](../reference/hyperledger_composer.html) con una aplicación Javascript | IBM<br> [Obtener ayuda![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/IBM-Blockchain/vehicle-manufacture/issues) |
|[Mercancías perecederas ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/clauseHQ/demo-clause-ibm-perishable-goods)| Los usuarios puede desplegar contratos legales que adquieren mercancías en una cadena de suministro basada en la entrega y en lecturas de temperaturas. <br>  <br> <!-- This sample leverages the [Toolchain tool service![External link icon](../images/external_link.svg "External link icon")](../images/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/ContinuousDelivery/index.html) to deploy the sample on your network automatically.--> | Definición de la red empresarial de [Hyperledger Composer](../reference/hyperledger_composer.html) con una aplicación Javascript | [ClauseHQ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](http://clause.io/)<br> [Obtener ayuda![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://github.com/clauseHQ/demo-clause-ibm-perishable-goods/issues) |

Las aplicaciones de ejemplo las crean los partners de IBM y de la comunidad. El soporte para muestras se proporcionará a través de los repositorios correspondientes de Github. Si tiene un problema, pulse el enlace **Obtener ayuda** junto al nombre del publicador y abra un problema en el repositorio Github para notificar al equipo relevante.

Para desplegar ejemplos, necesita una red blockchain en {{site.data.keyword.cloud_notm}} con el Plan inicial o el Plan empresarial, y configurar un canal y sus iguales. Para obtener más información, consulte [Gobierno de la red del Plan inicial](../get_start_starter_plan.html) y [Gobierno de la red del Plan empresarial](../get_start.html).


<!--

After you provision a Starter Plan network, you can deploy the sample applications in the Network Monitor, which automates the steps to enable sample applications to run on your network. You can also enable the samples step-by-step to learn the entire process of application deployment, which you need to follow when you deploy your own applications.

-->

<!--
## Deploying sample applications in Starter Plan

Starter Plan provides a simple approach to deploy sample applications by leveraging the Toolchain service on {{site.data.keyword.cloud_notm}} with just a few clicks. After you deploy and launch a sample application, it will run on your blockchain network automatically.

Starter Plan provides two sample applications for you to start with.

* **Marbles**

  The Marbles sample enables users to create virtual marbles with different properties and to transfer them with other users. For more information about Marbles, see [Marbles Demo ![External link icon](../images/external_link.svg "External link icon")](https://github.com/IBM-Blockchain/marbles).


* **Vehicle Manufacture**

  The Vehicle Manufacture sample enables users to go through the lifecycle of a virtual vehicle. For more information about this sample, see [Vehicle Manufacture ![External link icon](../images/external_link.svg "External link icon")](https://github.com/IBM-Blockchain/vehicle-manufacture).

Complete the following steps to deploy a sample application:

1. Enter the **Network Monitor** of your Starter Plan network. If you don't have one, see [Creating a network](../get_start_starter_plan.html#creating-a-network).

2. Open the "Try samples" screen in your Network Monitor. Choose the sample application that you want to deploy and click the **Deploy via Toolchain** button.

3. A Toolchain service configuration window opens. Ensure that all required tools are correctly integrated. Note that if you have more than one organizations, make sure that you enter the correct organization name. The organization name should be the email address that you use to sign up for the network.
    **Tip**: You must disable pop-up blockers so that the Toolchain service configuration page can open.


  If this is the first application that you deploy via Toolchain, you need to authorize Toolchain to access the GitHub repository.

  ![sampleappflow2](../images/sampleappflow2.png)

  After you click the "Authorize" button, you are taken to GitHub. If you don't have a GitHub account, you need to create one. Give Toolchain access to your repositories by entering your account information. If you don't want to give Toolchain this access, you can deploy the sample applications manually. For more information, see [Deploying sample applications manually](#deploy_sample_applications_manually).

5. Click the **Create** button at the bottom of the Toolchain page. This should take you back to the Network Monitor, where the deployment of Marbles should be in process. This process should take five to 10 minutes.

After the deployment completes, you can start to use the Marbles sample on your Starter Plan network.

Because this process creates a forked GitHub repository that you have access to and control over, you can make changes to Marbles in the forked repository and commit them. These commits will trigger an automatic build of your Marbles application and allow you to demo it in {{site.data.keyword.cloud_notm}}.
-->

<!--
## Deploying sample applications manually
{: #deploy_sample_applications_manually}

If you want to deploy sample applications without using the Network Monitor, ensure that you install all software prerequisites on your local file system. For more information, see [Setting up application development environment](../v10_application.html#setting-up-application-development-environment).

You also need a blockchain network on {{site.data.keyword.cloud_notm}} with either Starter Plan or Enterprise Plan, and configure a channel and its peers. For more information, see [Govern Starter Plan network](../get_start_starter_plan.html) and [Govern Enterprise Plan network](../get_start.html). After you provision a network and can deploy applications on it, retrieve the API endpoints of your network resources that your application will access. For more information, see [Adding network API endpoints to your application](../v10_application.html#adding-network-api-endpoints-to-your-application).

You can deploy one of the following sample applications to your network:

- **Marbles**

  In the Marbles application, multiple users can create marbles with different properties and transfer them to others. The Marbles application is written in JavaScript and the chaincode is written in Go.

  You can find the sample code and instructions in [Marbles in GitHub ![External link icon](../images/external_link.svg "External link icon")](https://github.com/IBM-Blockchain/marbles).

  Use the Bluemix instructions rather than the instructions for hosting Marbles locally and input the relevant information from your network. Note that the screen captures in the Marbles GitHub show the Enterprise Plan UI (since the Enterprise Plan supports only the manual path for deploying Marbles), which is a little different from the Starter Plan UI. Nevertheless both UIs have the same basic parts, and you can find the names of your peers, channels, and other service credential information in the appropriate screens.

- **Fabcar**

  In Fabcar, you can perform **queries** and **ledger updates** on car records in the ledger. Fabcar is written in JavaScript and the chaincode is written in Go.

  You can find sample code in [Fabric car in GitHub ![External link icon](../images/external_link.svg "External link icon")](https://github.com/hyperledger/fabric-samples/tree/release/fabcar), and instruction in [Writing Your First Application ![External link icon](../images/external_link.svg "External link icon")](http://hyperledger-fabric.readthedocs.io/en/latest/write_first_app.html).

- **Other applications**

  For more information about how to host your own applications inside {{site.data.keyword.cloud_notm}}, see [Hosting applications](../v10_application.html#hosting-applications).

-->

<!--
## Deleting a sample application

To delete a sample application that was acquired through the Toolchain process, navigate to where the sample lives in the UI. Because sample applications are instantiated on a channel, you can find the sample in channels. Click **Channels** on the left navigation to open the "Channels" screen. Click the relevant channel on which the sample is instantiated, and then click **Chaincode**. This displays chaincode that are instantiated on this channel.

If you click the chaincode of your application, you can see a **Delete** tab. However, clicking **Delete** alone does not delete the sample application, but delete only the chaincode container.  You also need to navigate to the {{site.data.keyword.cloud_notm}} dashboard and the Toolchain dashboard to delete the sample there.

-->
