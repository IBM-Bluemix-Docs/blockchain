---

copyright:
  years: 2019
lastupdated: "2019-05-16"

keywords: getting started tutorials, videos, web browsers

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

# Einführung in {{site.data.keyword.blockchainfull_notm}} Platform on {{site.data.keyword.cloud_notm}}
{: #ibp-v2-deploy-iks}

{{site.data.keyword.blockchainfull}} Platform on {{site.data.keyword.cloud_notm}} umfasst die {{site.data.keyword.blockchainfull_notm}} Platform-Konsole, bei der es sich um eine Benutzerschnittstelle handelt, mit der Sie Blockchain-Komponenten schneller bereitstellen und verwalten können. In diesem Lernprogramm wird beschrieben, wie Sie mit {{site.data.keyword.blockchainfull_notm}} Platform 2.0 beginnen und die Konsole verwenden können, um Blockchain-Komponenten in Ihrem {{site.data.keyword.cloud_notm}} Kubernetes Service-Cluster unter {{site.data.keyword.cloud_notm}} bereitzustellen und zu verwalten. Weitere Informationen zu Kubernetes und zu {{site.data.keyword.cloud_notm}} Kubernetes Service finden Sie unter [Kubernetes](/docs/services/blockchain/reference/k8s.html "Kubernetes").
{:shortdesc}

**Zielgruppe:** Dieser Abschnitt richtet sich an Systemadministratoren, die für die Einrichtung eines Kubernetes-Clusters on {{site.data.keyword.cloud_notm}} und für die Bereitstellung von {{site.data.keyword.blockchainfull_notm}} Platform verantwortlich sind.

Nachdem Sie {{site.data.keyword.blockchainfull_notm}} Platform mit Ihrem {{site.data.keyword.cloud_notm}} Kubernetes-Cluster verbunden haben, können Sie die Konsole starten, um Ihre Blockchain-Komponenten zu erstellen und zu verwalten und die folgenden wichtigen Vorteile zu nutzen:

- **Steuerung:** Sie steuern und verwalten Ihre Blockchain-Komponenten und Zertifikate von einer zentralen Konsole aus. Stellen Sie nur die Komponenten bereit, die für Ihr Unternehmen benötigt werden, und fügen Sie mehr hinzu, wenn Sie wachsen.
- **Flexible Kubernetes-basierte Bereitstellung:** Sie können die Optionen für die Rechenleistung (CPU, Hauptspeicher, Speicher) für Ihren Kubernetes-Cluster verwenden und integrierte HA- und DR-Optionen nutzen.


## Wichtige Hinweise
{: #ibp-v2-deploy-iks-considerations}

Stellen Sie vor der Bereitstellung der Konsole sicher, dass Sie die folgenden Aspekte verstehen:

- {{site.data.keyword.blockchainfull_notm}} Platform on {{site.data.keyword.cloud_notm}} basiert auf Hyperledger Fabric v1.4.
- Alle Peers, die mit der Konsole oder den APIs bereitgestellt werden, verwenden CouchDB als Statusdatenbank.
- Sie haben die Möglichkeit, Ihre {{site.data.keyword.blockchainfull_notm}} Platform-Serviceinstanz mit einem kostenlosen Kubernetes-Cluster zu verbinden, um das Angebot zu bewerten. Kapazität und Leistung sind jedoch begrenzt und Ihre Daten können nicht migriert werden. Der Cluster wird nach 30 Tagen gelöscht.
- Die Betatestversion ist zwar kostenlos, Sie müssen jedoch für Ihren Kubernetes-Cluster bezahlen, wenn Sie einen gebührenpflichtigen Cluster auswählen.
- Sie sind für das Management der Statusüberwachung, der Sicherheit und der Protokollierung Ihres Kubernetes-Cluster verantwortlich. Weitere Informationen dazu, was {{site.data.keyword.cloud_notm}} verwaltet und wofür Sie verantwortlich sind, finden Sie in dieser [Information ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/containers/cs_responsibilities.html#your-responsibilities-by-using-ibm-cloud-kubernetes-service "Cluster management responsibilities") .
- Sie sind auch für die Überwachung der Ressourcennutzung Ihres Kubernetes-Clusters über das Kubernetes-Dashboard verantwortlich. Wenn Sie die Speicherkapazität oder die Leistung Ihres Clusters erhöhen müssen, lesen Sie die Informationen zum [Ändern des vorhandenen Datenträgers ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/containers/cs_storage_file.html#change_storage_configuration "Ändern der Größe und E/A-Operationen pro Sekunde Ihrer vorhandenen Speichereinheit").
- Sie sind für die Verwaltung und Sicherung Ihrer Zertifikate und privaten Schlüssel verantwortlich. IBM speichert Ihre Zertifikate nicht im Kubernetes-Cluster.
- {{site.data.keyword.blockchainfull_notm}} Platform steht in ausgewählten Regionen zur Verfügung. Eine aktualisierte Liste hierzu finden Sie im Abschnitt zu den [Standorten von {{site.data.keyword.blockchainfull_notm}} Platform](/docs/services/blockchain/howto?topic=blockchain-ibp-regions-locations).
- Kubernetes muss in Ihrem {{site.data.keyword.cloud_notm}} Kubernetes-Cluster die Version 1.11 oder höher haben. Führen Sie die folgenden Anweisungen aus, um [ein Upgrade für Ihre neuen und vorhandenen Cluster](/docs/services/blockchain/howto/ibp-v2-deploy-iks.html#ibp-v2-deploy-iks-updating-kubernetes) auf diese Version zu aktualisieren.
- Sie müssen Speicher für Ihren Kubernetes-Cluster bereitstellen und als Standardspeicherklasse für den Cluster definieren. Dieser Speicher wird von Ihren Peer-, Anordnungsservice- und Zertifizierungsstellenknoten verwendet. Informationen zu den Entscheidungsfaktoren über den bereitzustellenden Speichertyp finden Sie im Abschnitt [Kubernetes-Speicher ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/containers?topic=containers-kube_concepts "Grundlagen zum Kubernetes-Speicher").

## Schulungsvideo
{: #ibp-v2-deploy-video}

Sehen Sie sich die folgende [Videoreihe]( http://ibm.biz/BlockchainPlatformSeries) an, um sich über die {{site.data.keyword.blockchainfull_notm}} Platform-Konsole und darüber zu informieren, wie Sie die ersten Schritte bei der Bereitstellung von {{site.data.keyword.blockchainfull_notm}} Platform on {{site.data.keyword.cloud_notm}} ausführen können.

## Vorbemerkungen
{: #ibp-v2-deploy-iks-prereq}

Vorbemerkungen:

- Stellen Sie sicher, dass ein [{{site.data.keyword.cloud_notm}} gebührenpflichtiges Konto ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog/services/blockchain "Catalog") vorhanden ist. Wenn Sie kein Konto haben:
   1. Klicken Sie auf die Schaltfläche **Registrieren** .
   2. Nach der Erstellung eines kostenfreien Testkontos führen Sie ein Upgrade auf ein **nutzungsabhängig Konto** durch, indem Sie **Verwalten** > **Abrechnung und Nutzung** > **Abrechnung** in der {{site.data.keyword.cloud_notm}}-Konsole aufrufen und auf **Kreditkarte hinzufügen** klicken.
   3. Stellen Sie sicher, dass der Benutzer sowohl die Administratorrolle als auch Managerrollen für den Kubernetes-Cluster besitzt, den er mit der zugehörigen Blockchain-Serviceinstanz verknüpfen wird. Weitere Informationen zu diesen Schritten finden Sie unter [Vorgehensweise zur Zuweisung von Kubernetes-Zugriffsrollen](#ibp-v2-deploy-iks-k8x-access-roles).

Wenn Sie planen, die Serviceinstanz im Kontext einer umfassenderen organisationsweiten Lösung zu verwenden, wird empfohlen, dass die teilnehmenden Organisationen eine funktionale E-Mail-Adresse verwenden, um ihr Netz zu erstellen. In diesem Fall ist der Zugriff auf das Netz nicht von der Verfügbarkeit der einzelnen Personen abhängig.
{:tip}  

- Wenn Sie einen vorhandenen {{site.data.keyword.cloud_notm}} Kubernetes Service-Cluster verwenden möchten, überprüfen Sie die Version von Kubernetes, und führen Sie bei Bedarf ein Upgrade auf Version 1.11 oder höher durch. Weitere Informationen zum Ermitteln der Version von Kubernetes, auf der Ihr Cluster ausgeführt wird, sowie zum Durchführen eines Upgrades auf eine höhere Version finden Sie im Abschnitt [Kubernetes-Version des Clusters aktualisieren](/docs/services/blockchain/howto/ibp-v2-deploy-iks.html#ibp-v2-deploy-iks-updating-kubernetes).

### Browser
{: #ibp-v2-deploy-iks-browsers}
Die folgende Liste enthält die Mindestanforderung für die Browsersoftware für die {{site.data.keyword.blockchainfull_notm}} Platform-Konsole:

- Chrome: aktuelle Version für Ihr Betriebssystem
- Firefox: aktuelle reguläre Versionen (keine ESR-Versionen) für Ihr Betriebssystem
- Safari: aktuelle Version für Mac
- Edge: Version 44.17763.1.0 oder höher

### Erforderliche Ressourcen
{: #ibp-v2-deploy-iks-resources-required}

#### Kostenlose Cluster
{: #ibp-v2-deploy-iks-resources-required-free}

Um die {{site.data.keyword.blockchainfull_notm}} Platform-Konsole in einem {{site.data.keyword.cloud_notm}} Kubernetes Service-Cluster bereitzustellen, müssen Sie sicherstellen, dass Ihr Kubernetes-Cluster die Mindestvoraussetzungen für die Hardwareressourcen erfüllt:

|Kubernetes-Cluster-Typ | Anwendungsfall | CPU | RAM | Workerknoten |
|-----------|------|-----|-----------------------|
|Standard (empfohlen) | Für MVPs geeignet | 4 (Gemeinsam genutzt) | 16 GB (gemeinsam genutzt)|Mehrere|
|Kostenlos** | Für eine Evaluierung geeignet | 2 | 4 GB | 1 |  
** Testen Sie {{site.data.keyword.blockchainfull_notm}} Platform für einen Zeitraum von 30 Tagen kostenlos, indem Sie Ihre {{site.data.keyword.blockchainfull_notm}} Platform-Serviceinstanz mit einem kostenlosen {{site.data.keyword.cloud_notm}} Kubernetes-Cluster verbinden. Die Leistung dieser Testversion ist jedoch in Bezug auf Durchsatz, Speicherkapazität und Funktionalität beschränkt. {{site.data.keyword.cloud_notm}} löscht Ihren Kubernetes-Cluster nach 30 Tagen. Eine Migration von Knoten oder Daten aus einem kostenlosen Cluster auf einen gebührenpflichtigen Cluster ist hierbei nicht möglich.

Diese Ressourcen sind für Tests und Versuchsreihen ausreichend. Das [Lernprogramm zum Aufbau eines Netzes](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network), in dem Sie zwei Peers, zwei Zertifizierungsstellen und einen Anordnungsknoten erstellen, beansprucht ungefähr 1,1 CPU, wobei etwas zusätzlicher Raum für Testzwecke (z. B. Erstellung mehrerer Kanäle mit jeweils separatem Ledger) gelassen wird. Wenn Sie einen kostenlosen Kubernetes-Cluster verwenden, beachten Sie, dass der Cluster nach Ablauf der 30-tägigen Testversion gelöscht wird und alle zugehörigen Assets entfernt werden. Auch ist die Leistung in einem kostenlosen Cluster deutlich langsamer.
{:note}

#### Gebührenpflichtige Cluster
{: #ibp-v2-deploy-iks-resources-required-paid}

Bereitstellungen von {{site.data.keyword.blockchainfull_notm}} Platform auf Produktionsebene erfolgen auf einem gebührenpflichtigen Cluster von {{site.data.keyword.cloud_notm}} Kubernetes Service. Die Größe und Konfiguration dieses Clusters hängt von den Anforderungen Ihres jeweiligen Anwendungsfalls ab. Größere Bereitstellungen müssen unbedingt in größeren Clustern erfolgen. Wie viel größer der Cluster als Ihre geplante Bereitstellung ist, liegt bei Ihnen. Vorzugsweise sollte etwas Freiraum gelassen werden, damit Peers und Anordnungsknoten zusätzlichen Kanälen beitreten und einen höheren Durchsatz übernehmen können, ohne dass zusätzliche Ressourcen in Ihrem Kubernetes-Cluster bereitgestellt werden müssen, **bevor** Sie die Größe Ihrer Knoten anpassen. Weitere Informationen zur Anpassung dieser Werte finden Sie unter [Neuzuordnung von Ressourcen](/docs/services/blockchain/howto/ibp-console-govern.html#ibp-console-govern-reallocate-resources).

Die Erstellung einer Erstbereitstellung von ausreichender Größe für weiteres Wachstum ist besonders wichtig für Benutzer, die sich gegen die Nutzung des [{{site.data.keyword.cloud_notm}} Kubernetes Service-Autoscalers ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/containers?topic=containers-ca#ca "{{site.data.keyword.cloud_notm}} Kubernetes Service-Autoscalers") entscheiden. Damit kann der Benutzer bei der Bereitstellung zusätzlicher Knoten und Pods entlastet werden.

Wenngleich es einfacher ist, genügend Ressourcen in {{site.data.keyword.cloud_notm}} Kubernetes Service bereitgestellt zu haben und die Pods und Workerknoten bedarfsgerecht erweitern zu können, ohne erst die Kubernetes-Clusterbereitstellung erhöhen zu müssen, verursachen größere Kubernetes-Clusterbereitstellungen entsprechend höhere Kosten. Benutzer müssen ihre Optionen sorgfältig prüfen und sich der Beeinträchtigungen bewusst sein, die sie mit der jeweiligen Option in Kauf nehmen.

Nachstehende Tabelle mit den aktuellen Standardwerten für den Peer, den Anordnungsknoten und die Zertifizierungsstelle gibt Ihnen einen Überblick darüber, wie viel Speicher und Rechenleistung Sie in Ihrem Cluster benötigen:

| **Komponente** (alle Container) | CPU  | Hauptspeicher (GB) | Speicher (GB) |
|--------------------------------|---------------|-----------------------|------------------------|
| **Peer**                       |  1,1          | 2,2                   | 200 (umfasst 100 GB für Peer und 100 GB für CouchDB)|
| **Zertifizierungsstelle**                         | 0,1            | 0,2                    | 20                     |
| **Anordnungsknoten**                    | 0,45           | 0,9                    | 100                    |

## Schritt 1: Erstellen Sie ein Verbindungsprofil für {{site.data.keyword.cloud_notm}} Platform
{: #ibp-v2-deploy-iks-create-service-instance}

Führen Sie die folgenden Schritte aus, um eine Serviceinstanz von {{site.data.keyword.blockchainfull_notm}} Platform 2.0 in {{site.data.keyword.cloud_notm}}zu erstellen.

1. Suchen Sie den [Blockchain-Service ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog/services/blockchain) im {{site.data.keyword.cloud_notm}} Katalog oder suchen Sie auf Ihrer {{site.data.keyword.cloud_notm}} Katalogseite nach `Blockchain`.
2. Sie sollten den **Service** für Ihre Instanz umbenennen, sodass Sie ihn in Zukunft einfacher erkennen können.
3. Bei der Betaversion ist **Dallas** die einzige verfügbare Region und kann nicht geändert werden.
4. Sie können die Felder für die Ressourcengruppe und die Tags unverändert lassen.
5. Klicken Sie auf **Erstellen**, um die Serviceinstanz bereitzustellen.

## Schritt 2: Stellen Sie {{site.data.keyword.blockchainfull_notm}} Platform bereit
{: #ibp-v2-deploy-iks-steps}

Folgen Sie der Anleitung zum Bereitstellen von {{site.data.keyword.blockchainfull_notm}} Platform sofort nach der Erstellung der Serviceinstanz.

1. Der Schritt **Willkommen & Voraussetzungen**. Wenn Sie bereits über einen vorhandenen {{site.data.keyword.IBM_notm}} Kubernetes Service-Cluster in der Region **Dallas** verfügen und ihn für Ihren Blockchain-Service verwenden möchten, wählen Sie das Kontrollkästchen aus. **Wenn Sie einen vorhandenen Cluster verwenden, können Sie den nächsten Schritt überspringen. Stellen Sie jedoch sicher, dass die Kubernetes-Version 1.11 oder höher verwendet wird.** Klicken Sie auf **Weiter**.
2. Der Schritt **Cluster erstellen**. Wenn Sie das Kontrollkästchen in Schritt 1 auswählen, um einen vorhandenen Kubernetes-Cluster zu verwenden, wird dieser Schritt übersprungen. Klicken Sie andernfalls auf **Neuen Cluster erstellen**, wodurch das {{site.data.keyword.cloud_notm}} Kubernetes-Dashboard zum Erstellen eines Clusters gestartet wird. Weitere Informationen finden Sie im Abschnitt [Einführung in {{site.data.keyword.cloud_notm}} Kubernetes Service ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/containers/getting-started.html). Planen Sie zusätzliche Zeit ein, um diesen Prozess abzuschließen.
  - Unabhängig vom ausgewählten Clustertyp müssen Sie bei der Betaversion die Position **Dallas** des Kubernetes-Clusters auswählen.
  - Wählen Sie **Standard-Cluster (empfohlen):** Wenn Sie eine längerfristige Option benötigen, die mehrere Knoten für die Hochverfügbarkeit enthält. **Achten Sie darauf, Kubernetes Version 1.11 oder höher auszuwählen.** Informationen zur Bereitstellung eines gebührenpflichtigen Clusters finden Sie unter [Standard-Cluster erstellen ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/containers?topic=containers-clusters#clusters_ui_standard "Standard-Cluster erstellen"). Bitte beachten Sie: Wenn Sie Hochverfügbarkeit oder Disaster-Recovery wünschen, müssen Sie eine Entscheidung über die Speicherklasse treffen, die Sie verwenden. Die `Standard-`-Speicherklasse für den Cluster wird von der dynamischen Bereitstellung verwendet. Auf diese Weise können Kunden eine beliebige Speicherklasse als Standard festlegen. Weitere Informationen finden Sie unter [Entscheidungshilfen zur Konfiguration der Dateispeicherung ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/containers?topic=containers-file_storage#file_predefined_storageclass "Entscheidungshilfen zur Konfiguration der Dateispeicherung").
  - Wählen Sie **Kostenloser Cluster:** aus, wenn Sie die Plattform für weniger als 30 Tage testen wollen. **Hinweis:** Beachten Sie, dass es nicht möglich ist, von einem kostenlosen Cluster auf einen gebührenpflichtigen Cluster zu migrieren. Der kostenlose Cluster bietet nur begrenzt Speicher und einen geringeren Transaktionsdurchsatz. Anweisungen dazu, was zu tun ist, wenn Ihr Kubernetes-Cluster abläuft, finden Sie in diesem Thema unter [Ablauf des Kubernetes-Clusters](/docs/services/blockchain/howto/ibp-console-manage.html#ibp-console-manage-console-cluster-expiration).
  - Weitere Informationen zu den Unterschieden zwischen den kostenlosen und gebührenpflichtigen Kubernetes-Clustern in {{site.data.keyword.cloud_notm}} finden Sie im Abschnitt [Vergleich von kostenlosen und Standard-Clustern ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/containers?topic=containers-cluster_types#cluster_types "Comparison of free and standard clusters").  

   Sie müssen in Ihrem Browser zu dieser Registerkarte zurückkehren, nachdem Sie den Cluster erstellt haben, damit Sie den Bereitstellungsprozess von {{site.data.keyword.blockchainfull_notm}} Platform 2.0 abschließen können.  
   {:important}  

  Sie müssen warten, bis Ihr Cluster erfolgreich bereitgestellt wurde. Klicken Sie dann auf die Schaltfläche **I Have a Cluster** (Ich habe einen Cluster).
3. Ihre Kubernetes-Version, die in Ihrem Cluster ausgeführt wird, muss die Version 1.11 oder höher haben. Führen Sie die folgenden [Schritte](/docs/services/blockchain/howto/ibp-v2-deploy-iks.html#ibp-v2-deploy-iks-updating-kubernetes) aus, um die Clusterversion zu überprüfen und gegebenenfalls ein Upgrade durchzuführen. Kehren Sie dann zurück und fahren Sie mit diesen Anweisungen fort.
4. Der Schritt **In Cluster bereitstellen**. Wählen Sie den Kubernetes-Cluster aus, auf dem Sie {{site.data.keyword.blockchainfull_notm}} Platform 2.0 bereitstellen möchten, aus der Dropdown-Liste aus, und klicken Sie auf **In Cluster bereitstellen**.  

  Wenn Ihr Kubernetes-Cluster in der Dropdown-Liste nicht sichtbar ist, kann dies durch die folgenden Bedingungen verursacht werden:
  - Der Prozess der Clustererstellung kann bis zu 60 Minuten in Anspruch nehmen. Wenn Sie einen Cluster erstellt haben, planen Sie zusätzliche Zeit ein, bis der Status Ihres Clusters **Normal** ist.
  - Cluster, die sich außerhalb der **Dallas**-Region befinden, sind nicht sichtbar und können nicht verwendet werden.
  - Stellen Sie sicher, dass Sie nicht die ESR-Version von Firefox verwenden. Wenn ja, wechseln Sie in einen anderen Browser, wie z. B. Chrome, und wiederholen Sie den Vorgang.

5. Der Schritt **Konsole starten**. Nachdem {{site.data.keyword.blockchainfull_notm}} Platform 2.0 erfolgreich bereitgestellt wurde, klicken Sie auf **{{site.data.keyword.blockchainfull_notm}} Platform starten**, um die {{site.data.keyword.blockchainfull_notm}} Platform-Konsole zu öffnen. Es kann ein paar Minuten dauern, bis die Schaltfläche aktiviert wird, während die Konsole bereitgestellt wird.

## (Optional) Der Konsole weitere Benutzer hinzufügen
{: #ibp-v2-deploy-iks-add-users}

Standardmäßig verwendet die Konsole [{{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/iam?topic=iam-iamoverview#iamoverview "IBM Cloud Identity and Access Management") als {{site.data.keyword.cloud_notm}}-Identitätsservice-Provider. Ihre {{site.data.keyword.blockchainfull_notm}} Platform-Konsole wird bereitgestellt, indem die E-Mail-Adresse des {{site.data.keyword.IBM_notm}}-Eigners als Administrator der Konsole konfiguriert wird. Als Administrator ist dieser Benutzer berechtigt, anderen Benutzern über ihre E-Mail-Adressen Zugriff auf die Konsole zu erteilen.  Lesen Sie hierzu die Anweisungen zur Vorgehensweise beim [Hinzufügen und Entfernen von Benutzern aus der Konsole](/docs/services/blockchain?topic=blockchain-ibp-console-manage-console#ibp-console-manage-console-add-remove).

## Nächste Schritte
{: #ibp-v2-deploy-iks-next-steps}

Jetzt ist Ihre Konsole einsatzbereit und Sie können mit dem [Lernprogramm zum Erstellen eines Netzes](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network) fortfahren.
Setzen Sie für die URL Ihrer Konsole ein Lesezeichen, sodass Sie sie zu einem späteren Zeitpunkt wieder aufrufen können. Andernfalls können Sie die Schritte ausführen, die im Abschnitt mit den [Nachinstallationsanweisungen](#ibp-v2-deploy-iks-post-install) aufgeführt sind, um die Konsole über Ihren Browser wieder aufzurufen.

## Kubernetes-Version Ihres Clusters aktualisieren
{: #ibp-v2-deploy-iks-updating-kubernetes}

Wenn Sie einen vorhandenen {{site.data.keyword.cloud_notm}} Kubernetes Service-Cluster verwenden, stellen Sie sicher, dass die Version von Kubernetes die Version 1.11 oder höher ist.

Sie können die Kubernetes-Version Ihres Clusters auf der [Kubernetes-Cluster-Seite ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/kubernetes/clusters) unter {{site.data.keyword.cloud_notm}} überprüfen, auf der alle Ihre Cluster in einer Tabelle aufgelistet sind.

Wenn die Version von Kubernetes nicht die Version 1.11 oder höher ist, müssen Sie die folgenden Schritte ausführen, um die Kubernetes-Version Ihres Clusters zu aktualisieren.

1. Klicken Sie auf das Überlaufmenü am Ende der Zeile und wählen Sie **Version aktualisieren** aus. Dieser Vorgang dauert etwa eine Stunde. Wenn die Version erfolgreich aktualisiert wurde, wird die aktualisierte Version Ihres Clusters in der Spalte **Kubernetes-Version** angezeigt.  
2. Wählen Sie die Kubernetes-Version 1.11 oder höher in der Dropdown-Liste der Kubernetes-Versionen aus und klicken Sie auf **Aktualisieren**.
3. Klicken Sie auf den Cluster und rufen Sie die Registerkarte **Workerknoten** auf. Wählen Sie das Kontrollkästchen vor dem Workerknoten aus, den Sie aktualisieren möchten, und klicken Sie in der Popup-Menüleiste auf **Kubernetes aktualisieren**. Wenn Ihr Cluster mehrere Workerknoten enthält, dann müssen alle diese Knoten aktualisiert werden.

  Aktualisierungen der Workerknoten können zu Ausfallzeiten Ihrer Apps und Services führen. Es wird ein neues Image Ihrer Workerknoten-Maschine erstellt und Daten werden gelöscht. Speichern Sie deshalb [Ihre Daten außerhalb des Pods ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/containers/cs_storage_planning.html#persistent_storage_overview).
  {:important}

![Kubernetes-Version aktualisieren](../images/update_k8s_version.gif)

Weitere Informationen zum Aktualisieren der Kubernetes-Version für einen {{site.data.keyword.IBM_notm}} Kubernetes Service-Cluster und für Workerknoten finden Sie im Abschnitt [Cluster, Workerknoten und Add-ons aktualisieren ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](/docs/containers?topic=containers-update#update).  

Sie müssen warten, bis die Aktualisierung abgeschlossen ist, bevor Sie [die Bereitstellung von {{site.data.keyword.blockchainfull_notm}} Platform 2.0](/docs/services/blockchain/howto/ibp-v2-deploy-iks.html#ibp-v2-deploy-iks-steps) fortsetzen können.

## Kubernetes-Zugriffsrollen zuweisen
{: #ibp-v2-deploy-iks-k8x-access-roles}

Der Benutzer, der die Blockchain-Serviceinstanz mit dem Kubernetes-Cluster verknüpft, muss über die Rollen "Administrator" und "Manager" in Kubernetes verfügen.
Zur Konfiguration dieses Zugriffs führen Sie die folgenden Schritte aus:
   1. Klicken Sie im {{site.data.keyword.cloud_notm}}-Dashboard auf die Dropdown-Liste **Verwalten** und dann auf **Zugriff (IAM)**.
   2. Klicken Sie im linken Navigationsmenü auf **Benutzer** und auf die ID des Benutzers, der die Serviceinstanz mit dem Kubernetes-Cluster verknüpft.
   3. Klicken Sie auf **Zugriffsrichtlinien** und dann auf **Zugriff zuweisen**.
   4. Klicken Sie auf die Kachel **Zugriff auf Ressourcen zuweisen**.
   5. Wählen Sie in der Dropdown-Liste **Services** die Option **Kubernetes Service** aus.
   6. Überprüfen Sie die **Administrator**- und die **Manager**-Rolle für diesen Benutzer.
   7. Klicken Sie auf **Zuweisen**.

![Kubernetes-Version aktualisieren](../images/k8sAccess.gif)

Weitere Informationen zur Zugriffssteuerung von Kubernetes finden Sie im Thema zur [Vorgehensweise zur Auswahl der richtigen Zugriffsrichtlinie und Rolle für Benutzer](/docs/containers?topic=containers-users#access_roles).

## Nachinstallationsanweisungen
{: #ibp-v2-deploy-iks-post-install}

### Konsole erneut aufrufen
{: #ibp-v2-deploy-iks-rtn-to-console}

Wenn Sie nach der Bereitstellung Ihrer Serviceinstanz erneut die Konsole aufrufen müssen, dann können Sie sie über das {{site.data.keyword.cloud_notm}}-Dashboard erneut öffnen.
1. Navigieren Sie in Ihrem Browser zu https://cloud.ibm.com/resources und melden Sie sich an.
2. Ihre {{site.data.keyword.blockchainfull_notm}} Platform-Serviceinstanz wird unter dem Twistie **Services** angezeigt. Suchen Sie nach der {{site.data.keyword.blockchainfull_notm}} Platform-Serviceinstanz, die von Ihnen bereitgestellt wurde, und klicken Sie darauf.
3. Klicken Sie in der daraufhin aufgerufenen Anzeige auf **{{site.data.keyword.blockchainfull_notm}} Platform starten**.

Ihre Konsole ist jetzt wieder sichtbar.

### Informationen zur Preisstruktur und Abrechnung
{: #ibp-v2-deploy-iks-pricing-billing}

- Im Abschnitt zur [Preisstruktur](/docs/services/blockchain/howto?topic=blockchain-ibp-saas-pricing) finden Sie Informationen zur Preisstruktur von {{site.data.keyword.blockchainfull_notm}} Platform.
- Ihre aktuellen Informationen zur Nutzung von {{site.data.keyword.cloud_notm}} stehen Ihnen über die [Kachel für die Nutzung ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/billing/ "Abrechnung und Nutzung") des {{site.data.keyword.cloud_notm}}-Dashboards zur Verfügung. Die Rechnung finden Sie unter [Abrechnungsinformationen ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/billing/billing-items "Rechnungspositionen"). Weitere Details zur Abrechnungsmethode bei {{site.data.keyword.blockchainfull_notm}} Platform finden Sie im Abschnitt zur [Abrechnung](/docs/services/blockchain/howto?topic=blockchain-ibp-saas-pricing#ibp-saas-pricing-billing).

### Serviceinstanz löschen
{: #ibp-v2-deploy-iks-delete-service-instance}

Wenn Sie Ihre Serviceinstanz nicht mehr benötigen, kann sie aus Ihrem Kubernetes-Cluster gelöscht werden, um Ressourcen freizugeben. Über das {{site.data.keyword.cloud_notm}}-Dashboard können Sie Ihre {{site.data.keyword.blockchainfull_notm}} Platform-Serviceinstanz löschen.

1. Navigieren Sie zu Ihrem [{{site.data.keyword.cloud_notm}}-Dashboard ![Symbol für externen Link](../images/external_link.svg "Symbol für externen Link")](https://cloud.ibm.com/ "Dashboard").
2. Lokalisieren Sie die Kachel **Ressourcenzusammenfassung** und klicken Sie auf **Services**.
3. Lokalisieren Sie unter dem Pfeilsymbol **Services** die Serviceinstanz, die Sie löschen möchten, und klicken Sie im Aktionsmenü auf **Löschen**.

Wenn das Löschen Ihrer Serviceinstanz fehlschlägt, ist der Kubernetes-Cluster möglicherweise nicht zugänglich. Wenn dies zutrifft, öffnen Sie ein [Support-Ticket](/docs/services/blockchain/ibmblockchain_support.html#blockchain-support-cases), damit die Serviceinstanz von einem Supportmitarbeiter gelöscht wird.
