---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-31"

keywords: Swagger APIs, authorize, service credentials, disable API access, IBM Cloud

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:gif: data-image-type='gif'}

# Cómo interactuar con la red con las API de Swagger
{: #ibp-swagger}

{{site.data.keyword.blockchainfull_notm}} Platform ofrece varias API REST en Swagger que puede utilizar para gestionar los nodos, canales, iguales y miembros de la red. Las aplicaciones pueden utilizar estas API para controlar los recursos de red importantes sin utilizar el Supervisor de red.

{:shortdesc}

Antes de empezar, debe crear una [instancia de servicio de {{site.data.keyword.blockchain}} Platform](https://cloud.ibm.com/catalog/services/ibm-blockchain-5-prod){: external} en {{site.data.keyword.cloud_notm}} y crear o unir una red blockchain del Plan inicial <!--or Enterprise Plan -->.


## Recuperación de credenciales de red
{: #ibp-swagger-retrieving-network-credentials}

Entre en el supervisor de red de la red blockchain y abra la pantalla "API" desde el navegador izquierdo. Verá sus credenciales de red para la API REST. Luego autorizará a las API mediante los valores "key" y "secret" que se muestran aquí y ejecutará las API con el valor "network_id" como parámetro. Pulse **Mostrar secreto** para revelar el valor del campo de secreto. Copie los valores de los campos de clave, secreto e id de red, que podrá utilizar más tarde en la IU de Swagger.

En la **Figura 1** se muestra la pantalla "API":
![Pantalla API](../images/API_screen_starter.png "Pantalla API")

Si utiliza el Plan inicial, puede cambiar de organización en el supervisor de red. Con el plan inicial, hay dos organizaciones configuradas de forma predeterminada. Cambiar de una organización a otra puede resultar útil para probar las API REST desde la perspectiva de cada organización. Para obtener las credenciales correspondientes a otra organización de la red, pulse su nombre en la esquina superior derecha de la consola del supervisor de red. En el menú que se abre, pulse la flecha desplegable que hay junto a la organización para ver todas las organizaciones. Seleccione la organización a la que desea cambiar y cuyas credenciales de red asociadas desea ver.

**Figura 2** muestra cómo cambiar de organización:

![Cambiar de organización](../images/switch_orgs_starter.gif "Cambiar de organización"){: gif}


## Autorización de las API de Swagger
{: #ibp-swagger-authorizing-swagger}

Pulse el enlace **IU de Swagger** de la pantalla "API" para abrir la IU de Swagger.  

En la IU de Swagger, pulse el botón **Autorizar** y aparecerá la ventana emergente de ventana de autorización. Escriba el valor de "key" y "secret" de las credenciales de red como nombre de usuario y contraseña y pulse **Autorizar** luego **Finalizado**. Ahora está preparado para ejecutar las API. Tenga en cuenta que, si se renueve el navegador, deberá volver a autorizar con sus credenciales.

Con la autenticación Basic Auth, las credenciales que especifique en la ventana Autorizar se guardan después de que pulse los botones **Autorizar** y **Finalizado** y se pasan en cada llamada de la API REST.

La **Figura 3** muestra el proceso para autorizar las API de Swagger:

![Autorizar API](../images/swaggerUIAuthorize.gif "Autorizar API"){: gif}


## Prueba de las API
{: #ibp-swagger-try-out}

Pulse la API REST que desea ejecutar y pulse el botón **Pruébelo**.

La **Figura 4** muestra el botón "Pruébelo" en la "IU de Swagger":

![Botón Pruébelo en la IU de Swagger](../images/swaggerUITryItOut.png "Botón Pruébelo en la IU de Swagger")

Después de pulsar el botón **Pruébelo**, puede especificar los parámetros necesarios para utilizar la API. Puede buscar `networkID` en las credenciales de red y buscar otros parámetros en el Supervisor de red. Después de especificar los parámetros, pulse **Ejecutar** para ejecutar la llamada de API REST en la red.

La **Figura 5** muestra parámetros en la "IU de Swagger":

![Parámetros de la IU de Swagger](../images/swaggerUIParams.png "Parámetros de la IU de Swagger")  

Después de pulsar **Ejecutar**, puede ver la respuesta de la llamada de API en la red. También puede ver un mandato CURL que puede invocar la API directamente desde la línea de mandatos.

La **Figura 6** muestra el cuerpo de respuesta de la API, el URL y el mandato CURL:

![Respuesta de API en la IU de Swagger](../images/swaggerUICurlResponse.png "Respuesta de API en la IU de Swagger")    

## Inhabilitación del acceso de API
{: #ibp-swagger-turn-off}

De forma predeterminada, todos los usuarios que tengan un rol que no sea Auditor en {{site.data.keyword.cloud_notm}} pueden ver y utilizar las
**credenciales de red** visibles en el panel de API de Swagger y, por lo tanto, pueden gestionar la red utilizando las API. No obstante, si prefiere no exponer las credenciales de red de la API de Swagger en la interfaz de usuario, puede copiar y proteger los valores de clave y de secreto existentes y generar nuevas credenciales que sean válidas para su uso con las API de Swagger. Se proporciona un distintivo, denominado resetCredentials, que le permite controlar el acceso realizando los pasos siguientes:

1. Siga los pasos para generar una nueva credencial de red tal como se describe en el
[Panel de control de credenciales de servicio](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-retrieve-id-token).
2. No obstante, en el recuadro **Añadir parámetros de configuración en línea**, pegue el valor siguiente:
   ```
   {
     "resetCredentials": true
   }
   ```
   {:codeblock}
3. Pulse **Añadir**.

Ahora, cuando cualquier usuario acceda al panel de API de Swagger desde la interfaz de usuario, la información de **Credenciales de red** de la interfaz de usuario incluirá un valor de clave y de secreto genérico que no es válido para gestionar la red. Las solicitudes de API enviadas utilizando estas credenciales no se procesarán.  

Si, posteriormente, desea exponer credenciales de red válidas en la interfaz de usuario, repita simplemente los pasos anteriores para generar una credencial nueva, pero deje en blanco el recuadro **Añadir parámetros de configuración en línea** en esta ocasión. No es necesario que especifique ningún parámetro.

Ahora, las credenciales válidas originales serán visibles en la información de **Credenciales de red** de la interfaz de usuario y se podrán utilizar para autenticar las API de Swagger.

## Consejos para la resolución de problemas
{: #ibp-swagger-troubleshooting}

### 401 No autorizado  
{: #ibp-swagger-401}

  Asegúrese de que tiene autorización sobre la API REST proporcionando sus credenciales de red. Para obtener más información, consulte [Autorización de las API de Swagger](/docs/services/blockchain/howto/swagger_apis.html#ibp-swagger-authorizing-swagger).

### Error 400: Solicitud errónea
{: #ibp-swagger-400}

  Algunas API acepten un argumento en el cuerpo de la solicitud que actúa como filtro para mostrar solo los resultados correspondientes a un determinado igual. Se proporciona un fragmento de código de ejemplo en el cuerpo que, si se utiliza, se debe editar para especificar el igual o la lista de iguales según los que desea filtrar. Para evitar este error, edite el fragmento de código para especificar un igual en la red o elimine el fragmento por completo.
