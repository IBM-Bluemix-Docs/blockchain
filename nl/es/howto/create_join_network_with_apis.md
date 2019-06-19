---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-20"

keywords: Swagger APIs, create a network, join a network, authentication credential

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:gif: data-image-type='gif'}

# Crear o unirse a una red con API de Swagger
{: #swagger-network}

{{site.data.keyword.blockchainfull}} Platform ofrece varias API REST que puede utilizar para crear o unirse a una red blockchain en {{site.data.keyword.cloud_notm}}. Puede probar estas API utilizando la [IU de Swagger](/docs/services/blockchain/howto/swagger_apis.html#ibp-swagger) asociada con la red.
{:shortdesc}


## Recuperación de la credencial de autenticación básica para la API
{: #swagger-network-retrieve-id-token}

Antes de empezar, tiene que crear una [instancia de servicio de {{site.data.keyword.blockchainfull_notm}} Platform](https://cloud.ibm.com/catalog/services/ibm-blockchain-5-prod){: external} con el Plan Inicial o el Plan de Empresa en {{site.data.keyword.cloud_notm}}.

Para utilizar API de Swagger para crear o unirse a una red, necesita una credencial de autenticación básica para asegurarse de que tiene acceso a la instancia de servicio en {{site.data.keyword.cloud_notm}}.

1. En el [panel de control de {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/resources){: external}, abra la instancia de servicio que ha creado.
2. Pulse **Credenciales de servicio** en el navegador izquierdo.
3. Pulse el botón "Nueva credencial" en la página **Credenciales de servicio** para crear una credencial nueva.
    1. Dé un nombre a la credencial, por ejemplo, *CreateJoin*.
    2. Escriba **{"type": "service_instance_token"}** en el campo "Añadir parámetro de configuración en línea".
    3. Pulse el botón **Añadir**.
    ![Recuperar credenciales de servicio](../images/service_credentials.gif "Recuperar credenciales de servicio"){: gif}
4. Una vez que se cree la nueva credencial, pulse **Ver credenciales** bajo la cabecera **ACTIONS** de esta credencial. El contenido de la credencial es similar al ejemplo siguiente:

    ```
    {
      "service_instance_id": "60cc757d-1234-7866-9893-491cec2d0eaa",
      "service_instance_token": "T8-W0rHv_vEya63P8KcVUwxAXXbDmihGcDRD5AcHVXGn6S2jbxx2LikPz8w26c3k",
      "description": "This token can be used with the IBP APIs to create or join a network. It can only be used once."
    }
    ```

    `service_instance_id` sirve como el ID de usuario de autenticación básica y `service_instance_token` sirve como la contraseña de autenticación básica. Utilice estos valores como la credencial de autenticación básica al invocar a las API **Crear red** o **Unirse a la red**.

    Si crea una red blockchain antes de seguir los pasos anteriores para crear una credencial de servicio, el contenido de la credencial también incluye la información de red y será similar al ejemplo siguiente:

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

    **Nota**: Para la API **Invitar**, la `clave` sirve como ID de usuario de autenticación básico y el `secreto` sirve como la contraseña de autenticación básica.


## Comprobando ubicaciones de red disponibles
{: #swagger-network-check-location}

Puede utilizar API para crear redes de blockchain solo en ubicaciones de red disponibles. Antes de crear una red, utilice la API siguiente para obtener una lista actual de las ubicaciones de red disponibles. No se necesitan credenciales para ejecutar esta API.

```
https://ibp-ep.us-south.ibm-blockchain-5-prod.cloud.ibm.com/api/v1/network-locations/available
```
{:codeblock}

Se devuelve una lista de ubicaciones de red disponibles que es similar a la del siguiente ejemplo:

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

Si tiene previsto crear una red, seleccione la ubicación donde desea crear la red de la lista devuelta por la API. Anote el valor de ``location_id`` y de ``swagger_url`` que están asociados con dicha ubicación.

Si piensa unirse a una red, tome nota del ``swagger_url`` asociado con el ``location_id`` especificado en el correo electrónico de invitación.

El valor ``swagger_url`` representa el punto final de la api que utilizará al crear o al unirse a una red utilizando las API siguientes.


## Creación de una red

**Nota**: Si utiliza el Plan inicial, no necesita crear una red con API porque se proporciona una red predeterminada al crear la instancia de servicio de blockchain en {{site.data.keyword.cloud_notm}}.

Si utiliza el Plan empresarial, debe realizar dos pasos para crear una red con API.

1. Cree una instancia de servicio de blockchain en {{site.data.keyword.cloud_notm}} con el Plan empresarial<!-- or Enterprise Plus Plan-->.  Recupere el ID de instancia de servicio y el token como nombre de usuario y contraseña de autenticación básica. Para obtener más información, consulte [Recuperación de credenciales de autenticación básica para API](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-retrieve-id-token).

2. Invoque la API **Crear red** utilizando estas credenciales de servicio. Emita esta API en el valor ``swagger_url`` de api recuperado de [Comprobación de las ubicaciones de red disponibles](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-check-location). Vaya al ``enlace swagger_url`` para utilizar la IU de Swagger para emitir la API Crear red, o emita mediante programación el mandato utilizando la dirección de URL sin ``/api-docs``. Por ejemplo,

    ```
    https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api/v1/networks
    ```
    {:codeblock}

**Parámetros**:
- `location_id`: El ID de una ubicación de red disponible. Especifique el valor de `location_id` anotado desde [Comprobando ubicaciones de red disponibles](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-check-location).
- `company_name`: El identificador como miembro en la red.
- `email`: Su dirección de correo electrónico para recibir notificaciones.
- `peers`: Número de iguales que desea crear para este miembro. Los valores válidos son del 0 al 6. También puede crear iguales para el miembro más adelante en la IU del Supervisor de red.
- `ledger_type`: El tipo de libro mayor de esta red. Los valores válidos son levelDB y couchDB. **levelDB** es el valor predeterminado.


## Invitar a nuevos miembros a una red

Después de crear una red blockchain, puede invitar a otros miembros a unirse a su red. Debe especificar el ID de la red a la que desea invitar a unirse a los nuevos miembros. La credencial de autenticación básica necesaria para invitar a un miembro es distinta a la que se utiliza en la API **Crear red**. <!--In order to get the basic auth information, you need to follow the same steps in "Retrieving basic auth information for API". --> Puede obtener la credencial para invitar a un miembro con la API **Recuperar credenciales de red** en la [IU de Swagger](/docs/services/blockchain/howto/swagger_apis.html#ibp-swagger-retrieving-network-credentials) o [recuperar información de autenticación básica para API](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-retrieve-id-token) desde la instancia de servicio en {{site.data.keyword.cloud_notm}}.

```
/networks/{networkID}/invite
```
{:codeblock}

**Parámetros**:
- `email`: La dirección de correo electrónico del miembro que se invitará a la red.
- `company_name`: El identificador que defina para el miembro que se unirá a la red. Los miembros invitados pueden cambiar sus identificadores al unirse a la red.

El miembro invitado recibirá una invitación por correo electrónico con instrucciones sobre cómo unirse a la red.


## Cómo unirse a una red

Si se le invita a unirse a una red blockchain, recibirá un correo electrónico de invitación de red que incluye el valor `location_id` y el valor `network id`.

1. Antes de unirse a la red, debe crear una instancia de servicio de {{site.data.keyword.blockchainfull_notm}} Platform y recuperar su ID y su señal de instancia de servicio como nombre de usuario y contraseña de autenticación básica. Para obtener más información, consulte [Recuperación de información de autenticación básica para API](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-retrieve-id-token).

2. [Compruebe las ubicaciones de red disponibles](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-check-location) para obtener el `swagger_url` para el `location_id` en el correo electrónico de invitación. Tendrá un aspecto similar al siguiente:

    ```
    https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api-docs
    ```
    {:codeblock}

3. Vaya al ``swagger_url`` para utilizar la IU de Swagger para emitir la API de Join, o enviar mediante programación la solicitud a Join utilizando el ``swagger_url``. Sustituya ``/api-docs`` por ``/api/v1/networks/[network_id]]/join``
y rellene el valor `network_id` utilizando el valor del correo electrónico de invitación. El URL resultante sería parecido al siguiente:

    ```
    https://ibmblockchain-v2-tor.1.secure.blockchain.ibm.com/api/v1/networks/56102acee0e4487889ef09db681bada0/join
    ```
    {:codeblock}

    **Nota**: Para la API de **Join**, utilice el ID y la señal de la instancia de servicio que recupera en el paso 1 como nombre de usuario y contraseña de autenticación básica.

**Parámetros**:
- `company_name`: El identificador como miembro en la red. Esto sustituirá el nombre del invitador asignado.
- `email`: Su dirección de correo electrónico para recibir notificaciones.  Esto debería coincidir con la dirección de correo electrónico de la notificación de invitación.
- `peers`: Número de iguales que desea crear para este miembro. Los valores válidos van del 0 al 6. También puede crear iguales para su miembro más adelante en el Supervisor de red.
