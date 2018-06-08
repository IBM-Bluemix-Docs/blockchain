---

copyright:
  years: 2017, 2018
lastupdated: "2018-5-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Despliegue de una red empresarial en el Plan inicial
{: #deploying-a-business-network}

Las redes empresariales se pueden desarrollar y desplegar en un entorno de Plan inicial mediante el entorno de desarrollo {{site.data.keyword.blockchainfull}} Platform y el conjunto de herramientas del desarrollador Hyperledger Composer.

Mediante el entorno del desarrollador, puede modelar rápidamente y probar redes empresariales de {{site.data.keyword.blockchain}} y desplegarlas en una instancia de la plataforma {{site.data.keyword.blockchainfull_notm}}.

## Antes de empezar

Asegúrese de leer los apartados [Acerca del Plan inicial](./starter_plan.html) e [Iniciación al Plan inicial](./get_start_starter_plan.html). Asegúrese también de tener instalado el [entorno del desarrollador de la plataforma {{site.data.keyword.blockchainfull_notm}}](./develop_install.html) y de haber creado una instancia del Plan inicial de la plataforma {{site.data.keyword.blockchainfull_notm}} siguiendo las instrucciones del [Gobierno de la red del Plan inicial](./get_start_starter_plan.html). Asegúrese de tener el nodo v8.9 o superior, npm v5.x, e Hyperledger Composer en v0.19.x.


## Paso uno: Recuperar el secreto de administración

1. Desde la pantalla de visión general del Plan inicial, pulse **Perfil de conexión** y, a continuación, descargue. Cambie el nombre de este archivo a 'connection-profile.json'.

2. Mueva este archivo para que esté en el mismo directorio que el archivo .bna.

3. Dentro del perfil de conexión, vaya hacia abajo hasta que vea 'registrar'. Dentro de 'registrar', bajo 'enrollId', hay una propiedad **enrollSecret**. Recupere el secreto y guarde una copia del mismo.

![D8KBag](https://i.makeagif.com/media/4-12-2018/D8KBag.gif)


## Paso dos: Crear una tarjeta de la entidad emisora de certificados

El secreto recuperado en el paso anterior se utilizará para crear una tarjeta de red empresarial para la autoridad emisora de certificados (CA). La tarjeta de CA se importará y se utilizará para intercambiar el **enrollSecret** por certificados válidos de la entidad emisora de certificados desde la autoridad de certificados del Plan inicial.

1. Mediante el **enrollSecret** anotado en el paso uno, ejecute el siguiente mandato para crear la tarjeta de red de visita de la entidad emisora de certificados:

        composer card create -f ca.card -p connection-profile.json -u admin -s ${enrollSecret}

2. Importe la tarjeta con el mandato siguiente:

        composer card import -f ca.card -c ca

3. Ahora que la tarjeta está importada, se podrá utilizar para intercambiar el **enrollSecret** para certificados válidos de la CA. Ejecute el siguiente mandato para solicitar certificados de la autoridad emisora de certificados:

        composer identity request --card ca --path ./credentials -u admin -s ${enrollSecret}

El mandato `composer identity request` crea un directorio `credentials` que contiene archivos `.pem` de certificado.

## Paso tres: Adición de los certificados a la instancia del Plan inicial

Los certificados se deben añadir a la instancia del Plan inicial. Para su comodidad, pueden añadirse mediante la IU de la plataforma {{site.data.keyword.blockchainfull_notm}}. Los certificados deben añadirse y luego los iguales se deben reiniciar, y a continuación los certificados se deben sincronizar en el canal. El certificado necesario es el archivo `admin-pub.pem` que se ha generado desde el mandato anterior, que está en el directorio `credentials`.

1. En la IU del Plan inicial, pulse el separador **Miembros**, luego **Certificados** y, a continuación, **Añadir certificado**. Vaya al directorio `credentials`, y copie y pegue el contenido del archivo `admin-pub.pem` en el recuadro de certificado. Envíe el certificado y reinicie los iguales. Nota: reiniciar los iguales lleva un minuto.

    ![jlEb2y](https://i.makeagif.com/media/4-12-2018/jlEb2y.gif)

2. A continuación, los certificados se deben sincronizar en el canal. Pulse el separador **Canales**, luego el botón **Acciones**, y luego **Sincronizar certificado** y **Enviar**.

![E-sVV5](https://i.makeagif.com/media/4-12-2018/E-sVV5.gif)

## Paso cuatro: Creación de una tarjeta de red empresarial de administración

Ahora que los certificados correctos se han sincronizado con los iguales, se pueden crear tarjetas de red empresarial, con permisos para instalar el entorno de ejecución de Hyperledger Composer y para iniciar el código de encadenamiento.

1. Cree una tarjeta de administración con los roles de administrador de canal y administrador de igual con el siguiente mandato:

        composer card create -f adminCard.card -p connection-profile.json -u admin -c ./credentials/admin-pub.pem -k ./credentials/admin-priv.pem --role PeerAdmin --role ChannelAdmin

    Esta tarjeta se utilizará para desplegar una red empresarial en el Plan inicial.

2. Importe la tarjeta creada en el paso anterior con el mandato siguiente:

        composer card import -f adminCard.card -c adminCard

## Paso cinco: Instalación e inicio de la red empresarial

A continuación, la tarjeta creada en el paso anterior se puede utilizar para instalar e iniciar una red empresarial. Para esta guía, instalaremos el ejemplo de red de fabricación de vehículos, bien utilice el ejemplo de fabricación de vehículos o bien instale su propia red empresarial, pero asegúrese de cambiar los nombres de redes empresariales especificados en los mandatos. El mandato para iniciar una red empresarial también creará una tarjeta. Para el Plan inicial, esta tarjeta se debe suprimir; el mandato de ejemplo asigna a esta tarjeta el nombre `delete_me.card`, de modo que se pueda distinguir fácilmente.

1. Instale el entorno de ejecución Hyperledger Composer con el siguiente mandato:

        composer network install -c adminCard -a vehicle-manufacture-network.bna

    Anote el número de versión de la red empresarial que se devuelve al ejecutar este mandato. Se necesitará en el paso siguiente.

2. Inicie la red empresarial con el mandato siguiente. Si obtiene un error, espere un minuto y vuelva a intentarlo. Utilice el número de versión del último paso después de la opción `-V`.

        composer network start -c adminCard -n vehicle-manufacture-network -V 0.0.1 -A admin -C ./credentials/admin-pub.pem -f delete_me.card

3. Suprima la tarjeta de red empresarial llamada `delete_me.card`.

4. Cree una nueva tarjeta de red empresarial y haga referencia a los certificados recuperados anteriormente con el siguiente mandato:

        composer card create -n vehicle-manufacture-network -p connection-profile.json -u admin -c ./credentials/admin-pub.pem -k ./credentials/admin-priv.pem

5. Importe la tarjeta de red empresarial con el siguiente mandato:

        composer card import -f ./admin@vehicle-manufacture-network.card

Ahora la red empresarial se ha desplegado en la instancia del Plan inicial.

## Paso seis: Hacer ping en la red empresarial para asegurarse de que se está ejecutando correctamente

1. Ejecute el mandato siguiente para hacer ping en la red empresarial:

        composer network ping -c admin@vehicle-manufacture-network

Para ver los registros de código de encadenamiento, pulse **Canales**, y luego seleccione el canal. Pulse la flecha desplegable para ver los registros, o el símbolo Acciones para ver con más detalle.

![fN-Yuj](https://i.makeagif.com/media/4-13-2018/fN-Yuj.gif)
