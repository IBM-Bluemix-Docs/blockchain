---

copyright:
  years: 2019
lastupdated: "2019-02-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Organisationen verwalten
{: #ibp-console-organizations}

***[Ist diese Seite hilfreich? Teilen Sie uns Ihre Meinung mit.](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***

Sie können die {{site.data.keyword.blockchainfull}} Platform-Konsole verwenden, um eine formale Organisationsdefinition zu erstellen, die als "Membership Service Provider (MSP)" bezeichnet wird. Die MSP-Definition Ihres Unternehmens ermöglicht es anderen Mitgliedern des Blockchain-Konsortiums, die Identität Ihrer Knoten und Anwendungen zu überprüfen. Ihre MSP-Definition enthält auch die Administratorzertifikate Ihrer Organisation.

Sie können die Konsole verwenden, um zu verwalten, welche Organisationen Mitglieder Ihres Netzes sind. Der Administrator des Anordnungsservices kann die Registerkarte "Organisationen" verwenden, um Mitglieder zum Blockchain-[Konsortium](/docs/services/blockchain/glossary.html#glossary-consortium) hinzuzufügen. Die Mitglieder des Konsortiums können dann die Konsole verwenden, um Mitglieder zu neuen oder vorhandenen Kanälen hinzuzufügen.

## Informationen zu MSPs
{: #console-organizations-about-msp}

The {{site.data.keyword.blockchainfull_notm}} Platform basiert auf Hyperledger Fabric und dient zur Erstellung genehmigter Blockchain-Netze. Dem Netz müssen die Teilnehmer bekannt sein, bevor sie Transaktionen übergeben und mit den Assets im Ledger interagieren können. Fabric erkennt die Identität durch eine Gruppe von eingeladenen Organisationen, die als Konsortium bezeichnet werden. Die Organisationen des Konsortiums sind in der Lage, gültige Berechtigungsnachweise an ihre Mitglieder auszugeben und sie zu Teilnehmern im Netz zu machen. Die Teilnehmer können dann Blockchain-Knoten betreiben und Transaktionen von Clientanwendungen übergeben.

Jede Organisation im Konsortium muss eine eigene Zertifizierungsstelle betreiben, die als Stammzertifizierungsstelle (Root-CA) bezeichnet wird. Diese Zertifizierungsstelle (oder ihre temporären Zertifizierungsstellen) erstellt alle Identitäten, die zu Ihrer Organisation gehören, und gibt jede Identität als öffentlichen und privaten Schlüssel aus. Diese Schlüssel werden von der Zertifizierungsstelle signiert und von den Mitgliedern Ihrer Organisation verwendet, um ihre Aktionen zu signieren und zu überprüfen. Wenn Sie dem Konsortium beitreten, können andere Organisationen Ihre Zertifizierungsstellen-Signatur erkennen und sicherstellen, dass Ihre Peers und Anwendungen gültige Teilnehmer sind. Weitere Informationen zur Mitgliedschaft in Hyperledger Fabric finden Sie im Konzeptthema [Mitgliedschaft ![External link icon](../images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/membership/membership.html "Membership") in der Fabric-Dokumentation.

Bevor Ihre Organisation Mitglied eines Konsortiums werden kann, muss sie eine Organisationsdefinition erstellen, die als **Membership Services Provider (MSP)** bezeichnet wird. Der MSP enthält die folgenden Informationen:
- Ein Zertifikat, das von Ihrer **Stammzertifizierungsstelle** signiert wurde. Dieses Zertifikat wird verwendet, um die Identität Ihrer Knoten, Kanäle und Anwendungen zu überprüfen.
- Ein Zertifikat, das von Ihrer **TLS-Zertifizierungsstelle** signiert wurde. Das TLS-Stammzertifikat ermöglicht Ihren Peers die Teilnahme an organisationsübergreifenden Gossip. Dies ist erforderlich, um die Vorteile der Features von [**Privaten ** Datensammlungen](/docs/services/blockchain/howto/ibp-console-smart-contracts.html#ibp-console-smart-contracts-private-data) und [Serviceerkennungen ![External link icon](../images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html "Serviceerkennungen") von Hyperledger Fabric zu nutzen.
- Die **MSP-ID**. Die MSP-ID ist der formale Name Ihrer Organisation innerhalb des Konsortiums. Sie müssen sich die MSP-ID für Ihre Knoten und Anwendungen merken.
- **Administratorzertifikate** von Ihren Identitäten für den **Peer-Administrator** und **Organisationsadministrator**. Diese Zertifikate werden an den Anordnungsservice übergeben und werden verwendet, um zu prüfen, welche Identitäten in Ihrem Unternehmen Kanäle erstellen oder bearbeiten dürfen. Wenn Sie Ihre Konsole zum Erstellen eines Anordnungsknotens oder Peers verwenden, werden die Administratorzertifikate im MSP innerhalb des neuen Knotens bereitgestellt. Diese Zertifikate können dann verwendet werden, um die Peers oder Anordnungsknoten von Ihrer Konsole oder von einer Clientanwendung aus zu betreiben.

## MSPs in der Konsole verwalten

Navigieren Sie zur Registerkarte **Organisationen**. Sie können diese Registerkarte verwenden, um [eine MSP-Definition zu erstellen](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-create-msp), indem Sie eine Zertifizierungsstelle verwenden, die in der Konsole vorhanden ist. Sie können diese Registerkarte auch zum [Importieren eines MSP](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-import-msp) verwenden, der von einer anderen Organisation erstellt wurde.

Sie können alle MSPs anzeigen, die Sie unter **Verfügbare Organisationen** erstellt oder importiert haben. Sie können die MSP-Definitionen auf der Registerkarte "Organisationen" für wichtige Funktionen in Ihrer Konsole verwenden:
- Wenn Sie Peerknoten oder Anordnungsknoten erstellen, wird der MSP Ihrer Organisation verwendet, um Administratorzertifikate für den neuen Knoten bereitzustellen.
- Wenn Sie der Administrator eines Anordnungsknotens sind, können Sie die MSPs verwenden, um [neue Organisationen zum Konsortium hinzuzufügen](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-add-consortium).
- Wenn Sie Mitglied des Konsortiums sind, können Sie die MSPs von anderen Konsortiumsmitgliedern in Ihre Konsole importieren und die Mitglieder dann zu neuen oder vorhandenen Kanälen hinzufügen.

## Einen MSP für Ihre Organisation erstellen
{: #console-organizations-create-msp}

Verwenden Sie die Registerkarte **Organisationen**, um eine MSP-Definition für Ihre Organisation zu generieren. Wenn Sie auf **MSP erstellen** klicken, wird ein Seitenfenster geöffnet, in dem Sie alle erforderlichen Informationen eingeben können: die Stammzertifizierungsstelle, die MSP-ID und Ihre Organisationsadministratoren.

- Verwenden Sie den Abschnitt **MSP-Details** in der Anzeige, um die MSP-ID Ihrer Organisation auszuwählen. Diese ID ist der formale Name, den andere Mitglieder des Netzes verwenden, um auf Ihre Organisation zu verweisen. **Speichern Sie Ihre MSP-ID.**

- Verwenden Sie den Abschnitt **Stammzertifizierungsstellendetails**, um die Stammzertifizierungsstelle (Root-CA) Ihrer Organisation auszuwählen. Dies ist die Zertifizierungsstelle (CA), die Sie verwendet haben (oder verwenden), um alle Knoten- und Anwendungsidentitäten zu erstellen, die zu Ihrer Organisation gehören. Wenn Sie temporäre Zertifizierungsstelle verwenden, ist dies die Zertifizierungsstelle, die Sie zum Erstellen dieser CAs verwendet haben. Wählen Sie Ihre Stammzertifizierungsstelle aus der Liste der CAs aus, die mit der Konsole verwaltet werden. Wenn Sie eine Zertifizierungsstelle über die Konsole erstellt haben, wird bei Auswahl einer Stammzertifizierungsstelle auch ein TLS-Stammzertifikat erstellt.

- Sie können auch den Abschnitt **Stammzertifizierungsstellendetails** verwenden, um eine der Administratorzertifikate Ihrer Organisation zu generieren. Bevor Sie die MSP-Definition Ihres Unternehmens erstellen, müssen Sie Ihre Organisations- und Knotenadministratoren bei Ihrer Stammzertifizierungsstelle registrieren. Sie müssen dann die folgenden Schritte ausführen, um diese Identitäten für den Betrieb des Netzes zu verwenden:

  1. Erstellen Sie ein öffentliches und ein privates Schlüsselpaar für jede Administratoridentität.
  2. Geben Sie den öffentlichen Schlüssel (Zertifikat) jeder Administratoridentität in der MSP-Definition an.
  3. Fügen Sie Ihrer Konsolen-Wallet die Identität hinzu. Die von der Konsole erstellten Knoten oder Kanäle verwenden die Zertifikate aus dem MSP, um zu prüfen, wer ein gültiger Administrator ist. Daher muss das gleiche öffentliche private Schlüsselpaar, das Sie zum Hinzufügen eines Administratorzertifikats zum MSP verwendet haben, in der Konsolen-Wallet gespeichert werden.

  Sie können die Anzeige **MSP-Definition erstellen** verwenden, um diese Aktionen für eine Ihrer Administratoridentitäten auszuführen. Nachdem Sie Ihre Stammzertifizierungsstelle ausgewählt haben, führen Sie die folgenden Schritte im Abschnitt **Administratorzertifikat Ihrer Organisation generieren** aus:
  1. Geben Sie die Eintragungs-ID und den geheimen Eintragungsschlüssel einer Administratoridentität ein, die bei Ihrer Stammzertifizierungsstelle registriert ist. Nachdem Sie die Eintragungs-ID und den geheimen Eintragungsschlüssel, wählen Sie einen Namen aus, um die Identität in Ihrer Konsolen-Wallet anzuzeigen.
  2. Klicken Sie auf **Generieren**. Dadurch wird eine neue Gruppe von öffentlichen und privaten Schlüsseln generiert und die Schlüssel werden automatisch zu Ihrer Konsolen-Wallet hinzugefügt. Sie können dann Ihre Administratoridentität in Ihrer Wallet finden, indem Sie den Namen verwenden, den Sie in dieser Anzeige ausgewählt haben. Diese Schlüssel werden nur im lokalen Speicher Ihres Browsers gespeichert. Wenn Sie also den Browser ändern, sind sie nicht mehr in der Konsolen-Wallet enthalten. Sie müssen die Identität aus Ihrem ursprünglichen Browser exportieren und sie in die Konsolen-Wallet Ihres neuen Browsers importieren.
  3. Klicken Sie anschließend auf **Exportieren**, um das Schlüsselpaar in Ihr Dateisystem herunterzuladen und zu sichern.

- Der Abschnitt **Administratoren (Optional)** des Seitenfensters enthält die öffentlichen Schlüssel Ihrer Administratoren. Das Zertifikat, das Sie mit dem Abschnitt **Administratorzertifikat Ihrer Organisation generieren** generiert haben, kann in der ersten Zeile des Felds **Administratorzertifikat** gefunden werden. Wenn Sie mehrere Administratoridentitäten für den Betrieb Ihres Netzes verwenden möchten, können Sie die Zertifikate zusätzlicher Knoten oder Organisationsadministratoren in die Felder **Administratorzertifikat** einfügen.

Da Ihre Administratorzertifikate mithilfe der MSP-Definition an Ihre Knoten und Kanäle übergeben werden, müssen Sie sicherstellen, dass jedes Administratorzertifikat Ihrer Knoten und Organisationen im MSP gespeichert wird. Wenn Sie mit der Konsole einen Anordnungsknoten, einen Peer oder einen Kanal erstellen, müssen Sie eine der Identitäten **zuordnen**, die Sie in Ihre Konsolen-Wallet mit den Administratorzertifikaten, die der MSP-Definition bereitgestellt wurden, exportiert haben. Wenn Sie den Abschnitt oder das Fenster **Identität zuordnen** auswählen, wählen Sie eine Identität aus, die Sie beim Erstellen der MSP-Definition generiert und in der Wallet gespeichert haben.

Nachdem Sie die Stammzertifizierungsstelle und die MSP-ID ausgewählt sowie die Administratorzertifikate erstellt haben, klicken Sie auf **MSP-Definition erstellen**, um die MSP-Definition zu erstellen. Sie wird jetzt als Organisation auf der Registerkarte "Organisationen" aufgeführt. Sie verwenden die MSP-Definition, wenn Sie Ihre Knoten bereitstellen und einem Blockchain-Konsortium beitreten.

## MSP importieren
{: #console-organizations-import-msp}

Nur der Anordnungsknoten-Administrator kann dem Konsortium neue Organisationen hinzufügen. Wenn Sie der Anordnungsknoten-Administrator sind, müssen Sie die MSP-Definitionen aller Organisationen erfassen, die zum Konsortium eingeladen wurden, und die MSPs in die Konsole importieren. Anschließend können Sie dem Anordnungsservice die MSPs hinzufügen, indem Sie den Anordnungsknoten verwenden.

Nachdem ein Administrator eine MSP-Definition erstellt hat, kann die Registerkarte "Organisationen" verwendet werden, um den MSP im JSON-Format in das lokale Dateisystem herunterzuladen. Dann kann Ihnen die MSP-JSON-Datei in einer Out-of-Band-Operation gesendet werden. Navigieren Sie zur Registerkarte **Organisationen** und verwenden Sie die Option **MSP-Definition importieren**, um die MSP-Datei in Ihre Konsole zu importieren. Sobald eine MSP-Definition im Abschnitt **Verfügbare Organisationen** angezeigt wird, können Sie zu Ihrem Anordnungsknoten navigieren, um [dem Konsortium die Organisation hinzuzufügen](docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-add-consortium).


## Einem Konsortium eine Organisation hinzufügen
{: #console-organizations-add-consortium}

Das Konsortium aus Organisationen wird vom Anordnungsservice gehostet.

Wenn Sie der Administrator des Anordnungsservices sind, können Sie die Konsole verwenden, um dem Konsortium eine Organisation hinzuzufügen. Navigieren Sie zu der Registerkarte **Knoten**, und klicken Sie auf den Anordnungsknoten. Klicken Sie in der Anzeige des Anordnungsknotens unter **Konsortiumsmitglieder** auf **Organisation hinzufügen**. Dadurch wird ein Seitenfenster geöffnet, in dem Sie eine Auswahl aus der Liste der verfügbaren MSP-Definitionen treffen können, die Sie [in Ihre Registerkarte "Organisationen" importiert haben](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-import-msp). Sie können auch die Option **JSON hochladen** verwenden, um die MSP-Definitionsdatei direkt zu importieren, die von einer anderen Organisation erstellt wurde.

## Kanal erstellen und bearbeiten

Nachdem dem Konsortium eine Organisation hinzugefügt wurde, kann der Anordnungsservice verwendet werden, um einen neuen Kanal zu erstellen oder zu einem Kanal hinzuzufügen. Die Informationen, die Ihnen die Teilnahme an einem Kanal ermöglichen, z. B. die Verbindung Ihrer Peers mit dem Kanal, die Instanziierung von Smart Contracts und die Übergabe von Transaktionen, werden mithilfe der MSP-Definitionen bereitgestellt.

Nachdem einem Konsortium eine Organisation hinzugefügt wurde, kann ein Kanal erstellt werden, indem die folgenden Schritte ausgeführt werden:

1. Importieren Sie den Anordnungsknoten, der das Konsortium hostet, in die Konsole. Sie müssen kein Administrator des Anordnungsknotens sein. Die Konsole muss jedoch den Namen und die Endpunktinformationen des Anordnungsknotens haben.
2. Importieren Sie die MSPs von Organisationen, die dem neuen Kanal hinzufügt werden sollen, über die Registerkarte "Organisationen" in die Konsole. **Hinweis:** Organisationen müssen dem Konsortium hinzugefügt werden, bevor sie einem Kanal hinzugefügt werden können.
3. Navigieren Sie zur Registerkarte **Kanäle** und klicken Sie auf **Kanal erstellen**. Dadurch wird ein Seitenfenster geöffnet, in dem Sie Kanalnamen, Mitgliedschaft und Kanalrichtlinien angeben können. Sie können alle Organisationen hinzufügen, die dem Konsortium zum neuen Kanal hinzugefügt wurden.

Weitere Informationen zu diesen Schritten finden Sie im Abschnitt [Kanal erstellen](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network-create-channel1) im Lernprogramm "Build a network" (Ein Netz erstellen).
