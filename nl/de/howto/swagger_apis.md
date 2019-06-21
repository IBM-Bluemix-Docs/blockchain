---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-16"

keywords: Swagger APIs, authorize, service credentials, disable API access, IBM Cloud

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Über Swagger-APIs mit dem Netz interagieren
{: #ibp-swagger}

{{site.data.keyword.blockchainfull_notm}} Platform stellt eine Reihe von REST-APIs in Swagger bereit, mit denen Sie die Knoten, Kanäle, Peers und Mitglieder Ihres Netzes verwalten können. Ihre Anwendungen können mithilfe dieser APIs wichtige Netzressourcen ohne den Network Monitor steuern.

{:shortdesc}

Bevor Sie beginnen, müssen Sie eine [{{site.data.keyword.blockchain}} Platform-Serviceinstanz ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog/services/ibm-blockchain-5-prod) in {{site.data.keyword.cloud_notm}} erstellen und ein Starter Plan-Blockchain-Netz erstellen oder an einem Starter Plan-<!--or Enterprise Plan -->Blockchain-Netz teilnehmen.


## Netzberechtigungsnachweise abrufen
{: #ibp-swagger-retrieving-network-credentials}

Wechseln Sie in den Network Monitor Ihres Blockchain-Netzes und öffnen Sie die Anzeige "APIs" im Navigator auf der linken Seite. Ihre Netzberechtigungsnachweise für die REST-APIs werden angezeigt. Später berechtigen Sie die APIs, indem Sie die hier angezeigten Werte des Schlüssels ("key") und des geheimen Schlüssels ("secret") verwenden und die APIs mit dem Parameter "network_id" (Netz-ID) ausführen. Klicken Sie auf **Geheimen Schlüssel anzeigen**, um den Wert des Felds für den geheimen Schlüssel ("secret") sichtbar zu machen. Kopieren Sie die Werte der Felder für Schlüssel, geheimen Schlüssel und Netz-ID, die Sie später in der Swagger-Benutzerschnittstelle verwenden können.

In **Abbildung 1** ist die Anzeige "APIs" zu sehen:
![Anzeige 'APIs'](../images/API_screen_starter.png "Anzeige 'APIs'")
*Abbildung 1. APIs*

Wenn Sie den Starter Plan verwenden, ist es möglich, im Network Monitor zwischen Organisationen zu wechseln. Mit dem Starter Plan werden standardmäßig zwei Organisationen konfiguriert. Das Wechseln zwischen Organisationen kann nützlich sein, um die REST-APIs aus der Perspektive jeder Organisation auszuprobieren. Zum Abrufen der Berechtigungsnachweise für eine andere Organisation in Ihrem Netz klicken Sie in der rechten oberen Ecke der Network Monitor-Konsole auf Ihren Benutzernamen. Klicken Sie in dem Menü, das sich daraufhin öffnet, auf den Dropdown-Pfeil neben der Organisation, um alle Organisationen anzuzeigen. Wählen Sie die Organisation aus, zu der Sie wechseln möchten, und zeigen Sie die zugeordneten Netzberechtigungsnachweise an.

**Abbildung 2** zeigt das Wechseln zwischen Organisationen:

![Wechseln zwischen Organisationen](../images/switch_orgs_starter.gif "Wechseln zwischen Organisationen")  
*Abbildung 2. Wechseln zwischen Organisationen*


## Swagger-APIs berechtigen
{: #ibp-swagger-authorizing-swagger}

Klicken Sie auf den Link für die **Swagger-Benutzerschnittstelle (UI)** in der Anzeige "APIs", um die Swagger-Benutzerschnittstelle zu öffnen.  

Klicken Sie in der Swagger-Benutzerschnittstelle auf die Schaltfläche **Berechtigen**. Das Berechtigungsfenster wird angezeigt. Geben Sie den Wert für den Schlüssel ("key") und den geheimen Schlüssel ("secret") in Ihren Netzberechtigungsnachweisen als Benutzername und Kennwort ein und klicken Sie auf **Berechtigen** und anschließend auf **Fertig**. Sie können jetzt die APIs ausführen. Beachten Sie, dass Sie sich mit Ihren Berechtigungsnachweisen erneut berechtigen müssen, wenn Sie Ihre Browseransicht aktualisieren.

Bei Verwendung der Basisauthentifizierung werden alle Berechtigungsnachweise, die Sie im Fenster **Berechtigen** angeben, nach dem Klick auf die Schaltflächen **Berechtigen** und **Fertig** gespeichert und mit jedem REST-API-Aufruf übergeben.

In **Abbildung 3** wird die Autorisierung von Swagger-APIs dargestellt:

![APIs autorisieren](../images/swaggerUIAuthorize.gif "APIs autorisieren")  
*Abbildung 3. Autorisierung von APIs*


## APIs ausprobieren
{: #ibp-swagger-try-out}

Klicken Sie auf die REST-API, die Sie ausführen möchten, und klicken Sie auf die Schaltfläche für das **Ausprobieren**.

In **Abbildung 4** ist die Schaltfläche für das Ausprobieren in der Swagger-Benutzerschnittstelle zu sehen:

![Schaltfläche für das Ausprobieren in der Swagger-Benutzerschnittstelle](../images/swaggerUITryItOut.png "Schaltfläche für das Ausprobieren in der Swagger-Benutzerschnittstelle")  
*Abbildung 4. Schaltfläche für das Ausprobieren in der Swagger-Benutzerschnittstelle*

Nach einem Klick auf die Schaltfläche für das **Ausprobieren** können Sie für die API erforderliche Parameter eingeben. Die `Netz-ID` finden Sie in Ihren Netzberechtigungsnachweisen, sonstige Parameter im Network Monitor. Klicken Sie nach der Parametereingabe auf die Schaltfläche für das **Ausführen**, um den REST-API-Aufruf für das gesamte Netz auszuführen.

**Abbildung 5** zeigt Parameter in der Swagger-Benutzerschnittstelle:

![Parameter in der Swagger-Benutzerschnittstelle](../images/swaggerUIParams.png "Parameter in der Swagger-Benutzerschnittstelle")  
*Abbildung 5. Parameter eingeben*  

Nach einem Klick auf die Schaltfläche für das **Ausführen** werden die Antworten zu dem API-Aufruf für das Netz angezeigt. Ihnen wird auch ein cURL-Befehl angezeigt, mit dem die API direkt über die Befehlszeile aufgerufen werden kann.

In **Abbildung 6** sind der Hauptteil der API-Antwort, die URL und der cURL-Befehl zu sehen:

![API-Antwort in der Swagger-Benutzerschnittstelle](../images/swaggerUICurlResponse.png "API-Antwort in der Swagger-Benutzerschnittstelle")  
*Abbildung 6. API-Antwort*    

## API-Zugriff inaktivieren
{: #ibp-swagger-turn-off}

Standardmäßig können alle Benutzer mit einer Nicht-Auditorrolle in IBM Cloud die **Netzberechtigungsnachweise** anzeigen und verwenden, die in der Swagger-API-Anzeige sichtbar sind, und somit Ihr Netz mittels der APIs verwalten. Wenn Sie jedoch Ihre Swagger-API-Netzberechtigungsnachweise nicht in der Benutzerschnittstelle bereitstellen möchten, können Sie Ihre vorhandenen Werte für Schlüssel und geheimen Schlüssel kopieren und sichern und neue Berechtigungsnachweise generieren, die für die Verwendung mit Swagger-APIs nicht gültig sind. Ein Flag mit dem Namen "resetCredentials" wird bereitgestellt, mit dem Sie anhand der folgenden Schritte den Zugriff steuern können:

1. Befolgen Sie die Schritte zum Generieren eines neuen Netzberechtigungsnachweises, wie im [Dashboard für Serviceberechtigungsnachweise](/docs/services/blockchain/howto/create_join_network_with_apis.html#swagger-network-retrieve-id-token) beschrieben.
2. Fügen Sie jedoch im Feld **Inline-Konfigurationsparameter hinzufügen** den folgenden Wert ein:
   ```
   {
     "resetCredentials": true
   }
   ```
   {:codeblock}
3. Klicken Sie auf **Hinzufügen**.

Wenn nun ein beliebiger Benutzer über die Benutzerschnittstelle auf die Swagger-API-Anzeige zugreift, enthalten die Informationen der **Netzberechtigungsnachweise** einen generischen Schlüssel und einen Wert für einen geheimen Schlüssel, der für die Verwaltung des Netzes ungültig ist. API-Anforderungen, die mit diesen Berechtigungsnachweisen übergeben werden, werden nicht verarbeitet.  

Wenn Sie zu einem späteren Zeitpunkt gültige Netzberechtigungsnachweise in der Benutzerschnittstelle zugänglich machen möchten, wiederholen Sie einfach die oben beschriebenen Schritte, um einen neuen Berechtigungsnachweis zu generieren. Dieses Mal können Sie jedoch das Feld **Inline-Konfigurationsparameter hinzufügen** leer lassen. Sie müssen keine Parameter angeben.

Nun werden die ursprünglichen gültigen Berechtigungsnachweise in den **Netzberechtigungsnachweis**-Informationen in der Benutzerschnittstelle angezeigt und können zur Authentifizierung der Swagger-APIs verwendet werden.

## Tipps zur Fehlerbehebung
{: #ibp-swagger-troubleshooting}

### 401 Keine Berechtigung  
{: #ibp-swagger-401}

  Stellen Sie sicher, dass Sie die REST-API durch Bereitstellen Ihrer Netzberechtigungsnachweise berechtigt haben. Weitere Informationen finden Sie unter [Swagger-APIs berechtigen](/docs/services/blockchain/howto/swagger_apis.html#ibp-swagger-authorizing-swagger).

### 400 Fehler: Falsche Anforderung
{: #ibp-swagger-400}

  Einige APIs akzeptieren möglicherweise ein Argument im Hauptteil (Body) der Anforderung, das als Filter für die Anzeige von Ergebnissen nur für einen bestimmten Peer verwendet wird. Ein Beispielausschnitt wird im Hauptteil bereitgestellt. Wenn dieser Ausschnitt verwendet wird, muss er bearbeitet werden, um den Peer bzw. die Liste von Peers anzugeben, nach denen Sie filtern möchten. Zur Vermeidung dieses Fehlers bearbeiten Sie entweder den Ausschnitt, um einen Peer in Ihrem Netz anzugeben, oder Sie entfernen den Ausschnitt völlig.
