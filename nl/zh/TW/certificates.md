---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 在 {{site.data.keyword.blockchainfull_notm}} 平台上管理憑證
{: #certificates}


***[此頁面有幫助嗎？請告訴我們。](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***


「{{site.data.keyword.blockchainfull}} 平台」是以 Hyperledger Fabric 為基礎，並建置具有許可權的區塊鏈網路。參與者稱為網路成員，而且其活動以及對網路資源的存取會持續進行驗證。參與者的身分是以信任的 x509 數位憑證表單提供。驗證是由基礎公開金鑰以及簽署/驗證作業所提供，而這些作業可以保護網路內的交易及管理。
{:shortdesc}

「{{site.data.keyword.blockchainfull_notm}} 平台」會管理大部分的憑證作業，無需使用者處理其憑證。不過，有時您必須管理容許您與網路通訊的憑證，例如開發應用程式或利用遠端對等節點擴充您的網路。下列是「憑證管理中心」及基礎憑證基礎架構的簡短指南。本指導教學可協助您瞭解您將使用的憑證以及您需要執行的作業。

## 憑證管理中心
{: #network-ca}

「憑證管理中心 (CA)」會在網路上提供身分。CA 可以視為公開信任的公證人，其充當多方之間的信任錨點。系統會將封裝其數位身分的主要 CA 所簽署的憑證提供給網路中的所有實體。此憑證是信任網路上執行之所有簽署及驗證作業的根源。如需如何使用憑證管理中心來建立身分的詳細資料，請參閱 [Hyperledger Fabric 文件![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://hyperledger-fabric.readthedocs.io/en/latest/identity/identity.html)。

網路中的每一個成員都擁有自己的 CA，這是從網路的主要 CA 發出憑證。這個與主要 CA 的關聯會為您的組織建立信任錨點。您的組織 CA 會簽署您組織所擁有之所有實體（例如管理者、對等節點或應用程式）的要求。如果您想要將遠端對等節點或新的應用程式新增至網路，則需要向「憑證管理中心」登錄新身分（登錄）。然後， CA 可以為新實體提供其與網路互動所需的憑證（登記）。

### 使用網路監視器登錄
{: #ca-panel}

您可以使用「{{site.data.keyword.blockchainfull_notm}} 平台網路監視器」，來檢視向您的 CA 登錄的身分，以及新增身分。請導覽至「網路監視器」的「憑證管理中心」畫面。此畫面會顯示已向您的 CA（包括您的組織管理者、對等節點及用戶端應用程式）登錄的所有身分。若要在您的組織中登錄新身分，請按一下畫面頂端的**新增使用者**按鈕。即會開啟蹦現視窗，並顯示登錄新身分所需的下列欄位。
  - **ID：**這將是新身分的名稱，有時稱為 `enroll ID`。請**儲存此值**，以供您配置遠端對等節點或登記新的應用程式時使用。
  - **密碼：**這將是新身分的密碼，有時稱為 `enroll Secret`。請**儲存此值**，以供您配置遠端對等節點或登記新的應用程式時使用。  
  - **類型：**選取要登錄的身分類型：對等節點或用戶端應用程式。
  - **連結：**這將是組織（例如 `org1`）內身分所屬的連結。
  - **登記數上限：**您可以使用此欄位，限制您可以使用此身分來登記或產生憑證的次數。如果將此欄位留白，則該值預設為數目無限制的登記。

如果您要部署[遠端對等節點](howto/remote_peer.html)，則可以使用這個畫面來登錄新的對等節點身分。或者，如果您要開發應用程式，將交易提交給您的網路，則可以登錄用戶端。請造訪[開發應用程式指導教學](v10_application.html)，來進一步瞭解如何使用 Fabric SDK 與平台搭配。

### 產生用戶端憑證（登記）
{: #enrollment}
將協力廠商用戶端連接至「{{site.data.keyword.blockchainfull_notm}} 平台」之前，您將需要進行鑑別。此處理程序稱為登記，其會產生必要憑證、私密金鑰及公用憑證（也稱為登記憑證或 signCert）。您的用戶端只要與網路通訊時，將需要這些憑證。將呼叫提交至網路的任何用戶端都需要使用私密金鑰來簽署有效負載，並附加適當簽署的 x509 憑證。

造訪[開發應用程式指導教學](v10_application.html)，以瞭解如何[使用 Fabric Node SDK 登記](v10_application.html)。使用 SDK 登記會產生 signCert、用來建立 signCert 的公開金鑰，以及私密金鑰。

您也可以使用「Fabric CA 用戶端」，從[指令行](#enroll-register-caclient)產生憑證。「Fabric CA 用戶端」會在「成員資格服務提供者 (MSP)」資料夾內傳回更完整的憑證集。此資料夾包含由 CA 所簽署的主要憑證，這些憑證會關聯於您的連結、私密金鑰及 signCert。若要進一步瞭解 MSP 及此資料夾所含內容，請參閱下面的[成員資格服務提供者](#msp)小節。

### 將簽署憑證上傳至 {{site.data.keyword.blockchainfull_notm}} 平台
{: #upload-certs}

應用程式需要有效的簽章憑證，才能將交易提交至網路。不過，如果客戶想要操作網路，方法是例如在對等節點上安裝鏈碼，或將對等節點加入至頻道，則用戶端需要被辨識為管理者。每一個元件皆可辨識由管理者所擁有的一組 signCert。如果您需要從用戶端操作網路，則需要上傳您的 signCert，並將它新增至管理憑證的清單。您可以在平台上執行此動作，方法是在「網路監視器」的[「概觀」畫面](v10_dashboard.html#members)的**憑證**標籤中上傳您的 signCert。請按下上傳之後出現的重新啟動按鈕，將此憑證與您的對等節點同步。之後，您的用戶端可被辨識為網路的管理者。

<!----
When you add an organization to a channel, this will upload the organization signCert to the channel MSP. Synching the Sign Certs does something.
--->

## 使用 TLS 憑證
{: #tls}

[傳輸層安全 ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10660_.htm) (TLS) 內嵌在 Hyperledger Fabric 的信任模型中。「{{site.data.keyword.blockchainfull_notm}} 平台」上的所有元件都會使用 TLS 來彼此鑑別及通訊。因此，您需要將平台發出的 TLS 憑證附加至您的呼叫，以便驗證及加密您的通訊。本指導教學中討論的其他憑證可保護您與網路進行交易，以及管理網路的能力。TLS 憑證用來保護您對網路的呼叫。

TLS 憑證是由平台公開發出，且對所有網路元件都是相同的。您可以使用下列鏈結來下載 TLS 憑證，視您的成員資格計劃和雲端位置而定。您也可以在[憑證設定檔](v10_dashboard.html#enterprise-connection-profile "憑證設定檔")中找到 TLS 憑證。此憑證可以位於任何位置，只要您從應用程式或指令行參照它即可。

- 入門範本方案的主要 TLS 憑證  
  - 美國：[us01.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/us01.blockchain.ibm.com.cert "us01.blockchain.ibm.com.cert")；[us02.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/us02.blockchain.ibm.com.cert "us02.blockchain.ibm.com.cert")
  - 英國：[uk01.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/uk01.blockchain.ibm.com.cert "uk01.blockchain.ibm.com.cert")；[uk02.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/uk02.blockchain.ibm.com.cert "uk02.blockchain.ibm.com.cert")
  - 雪梨：[aus01.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/aus01.blockchain.ibm.com.cert "aus01.blockchain.ibm.com.cert")；[aus02.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/aus02.blockchain.ibm.com.cert "aus02.blockchain.ibm.com.cert")
- [企業方案的主要 TLS 憑證 ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://blockchain-certs.mybluemix.net/3.secure.blockchain.ibm.com.rootcert)

所有「{{site.data.keyword.blockchainfull_notm}} 平台」網路都會使用伺服器端 TLS，其中的網路需要鑑別用戶端。「企業方案」網路也可以啟用相互 TLS ，讓用戶端和伺服器彼此鑑別，以進一步保護您的應用程式。用戶端 TLS 憑證（適用於「相互 TLS」）是由用戶端 CA 發出，且對您的網路是唯一的。如果您使用「企業方案」網路，建議您啟用相互 TLS。如需相互 TLS 的相關資訊，請參閱下列[指示](v10_dashboard.html#mutual-tls "相互 TLS 指示")。

## 成員資格服務提供者 (MSP)
{: #msp}

「{{site.data.keyword.blockchainfull_notm}} 平台」的元件透過「成員資格服務提供者 (MSP)」來耗用身分。MSP 會使 CA 發出的憑證與網路及頻道角色產生關聯。如需 MSP 的相關資訊，請參閱 [Hyperledger Fabric 文件中的成員資格概念主題 ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://hyperledger-fabric.readthedocs.io/en/latest/membership/membership.html "Hyperledger Fabric 文件中的成員資格概念主題")。

Fabric 內的 MSP 資料夾具有已定義的結構。使用「Fabric CA 用戶端」登記時，用戶端會將憑證儲存在本端檔案系統上具有下列子資料夾的 MSP 資料夾中：

- **cacerts：**此資料夾包含網路主要 CA 的主要憑證。
- **intermediatecerts：**這些是網路的中繼 CA 的憑證。這些中繼 CA 會鏈結至主要 CA，並形成信任鏈。每一個「企業方案」組織都有兩個中繼 CA，用於失效接手和高可用性。
- **signcerts：**此資料夾包含您的公用簽署憑證，也稱為您的 signCert 或登記憑證。當您從指令行參照 MSP 目錄，或使用 SDK 建置使用者環境定義物件時，此憑證會附加至您對網路的呼叫（例如鏈碼呼叫）。如果您要從 SDK 或指令行操作網路，則可以將此憑證上傳至平台。
- **keystore：**此資料夾包含您的私密金鑰。當您從指令行參照 MSP 目錄，或使用 SDK 建置使用者環境定義物件時，此憑證用來簽署您對網路的呼叫。請確保這個金鑰安全，以保護您的網路及資料。

您也可以使用「網路監視器」及 Swagger API，建置可由「Fabric CA 用戶端」參照的 MSP 資料夾。

- **cacerts** 及 **intermediatecerts**：您可以對 MSP API 發出 Get 要求，以利用 [Swagger API](howto/swagger_apis.html) 來提取這些憑證。
- **signcerts** 及 **keystore**：您可以按一下「憑證管理中心」畫面上的**產生憑證**按鈕，來產生這些憑證。即會開啟一個蹦現視窗，其中列出兩個憑證。複製**憑證**並儲存在 signCert 中，以及複製**私密金鑰**並儲存在金鑰儲存庫中。將這些憑證保存在安全的地方，因為它們不會儲存在平台上。

許多 Fabric 元件在其 MSP 資料夾內包含其他資訊。比方說，如果您操作遠端對等節點，則可能會看到下列資料夾：

- **admincerts：**此資料夾包含此組織或元件的管理者清單。如果您是從指令行或 SDK 來操作遠端對等節點，則需要將簽署憑證上傳至此資料夾。
- **tls：**這是儲存 TLS 憑證的資料夾，而這些憑證用於與其他網路元件通訊。

如需 MSP 結構的相關資訊，請參閱 Hyperledger Fabric 文件中的[成員資格 ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://hyperledger-fabric.readthedocs.io/en/latest/membership/membership.html "成員資格") 及[成員資格服務提供者 ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://hyperledger-fabric.readthedocs.io/en/latest/msp.html "成員資格服務提供者")。

## 使用 Fabric CA 用戶端登記及登錄
{: #enroll-register-caclient}

您也可以使用「Fabric CA 用戶端」來產生憑證，並向「憑證管理中心」登錄新的身分。下面的指示會使用您的管理者身分來產生憑證，然後使用那些憑證來登錄新的用戶端。使用「Fabric CA 用戶端」登記時，將產生[「成員服務提供者」區段](#msp)中說明的憑證。

### 使用 Fabric CA 用戶端登記
{: #enroll-app-caclient}

1. 將 [fabric-ca binaries](https://nexus.hyperledger.org/content/repositories/releases/org/hyperledger/fabric-ca/hyperledger-fabric-ca/) 下載至本端機器，並解壓縮它們，然後將其移至 `$HOME/fabric-ca-platform/` 這類的資料夾。切換至您已將用戶端二進位檔移至其中的目錄，以便您可以在指令中直接參照它。
    ```
    cd $HOME/fabric-ca-platform/
    ```

2.  設定用戶端可在其中建立金鑰的路徑。請務必移除過去嘗試建立的配置資料。如果您之前未執行 `enroll` 指令，則 `msp` 資料夾與 `.yaml` 檔不存在。
    ```
    export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca-platform
    rm -rf $FABRIC_CA_CLIENT_HOME/fabric-ca-client-config.yaml
    rm -rf $FABRIC_CA_CLIENT_HOME/msp
    ```

3. 根據您所使用的服務方案、位置及叢集，從 {{site.data.keyword.cloud_notm}} 下載 TLS 憑證。
  - 入門範本方案的主要 TLS 憑證  
    - 美國：[us01.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/us01.blockchain.ibm.com.cert "us01.blockchain.ibm.com.cert")；[us02.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/us02.blockchain.ibm.com.cert "us02.blockchain.ibm.com.cert")
    - 英國：[uk01.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/uk01.blockchain.ibm.com.cert "uk01.blockchain.ibm.com.cert")；[uk02.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/uk02.blockchain.ibm.com.cert "uk02.blockchain.ibm.com.cert")
    - 雪梨：[aus01.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/aus01.blockchain.ibm.com.cert "aus01.blockchain.ibm.com.cert")；[aus02.blockchain.ibm.com.cert ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](http://blockchain-certs.mybluemix.net/aus02.blockchain.ibm.com.cert "aus02.blockchain.ibm.com.cert")
  - [企業方案的主要 TLS 憑證 ![外部鏈結圖示](images/external_link.svg "外部鏈結圖示")](https://blockchain-certs.mybluemix.net/3.secure.blockchain.ibm.com.rootcert)

  將內容儲存至資料夾，例如 ``$HOME/tls``。此步驟可讓資料流在通訊連線上加密。

4. 從「網路監視器」的「概觀」畫面中，開啟**連線設定檔** JSON 檔案，並尋找下列變數：
  * CA 的 URL：``certificateAuthorities`` 下的 ``url``
  * 管理使用者 ID：``enrollId``
  * 管理密碼：``enrollSecret``
  * CA 名稱：``caName``

5. 您可以使用 Fabric CA 用戶端，搭配下列指令來傳入 TLS 憑證路徑及上述四個字串，以將 `enroll` 呼叫傳送至「憑證管理中心」：
  ```
  ./fabric-ca-client enroll -u https://<enroll_id>:<enroll_password>@<ca_url_with_port> --caname <ca_name> --tls.certfiles <tls_cert_path>
  ```
  {:codeblock}

  您需要在將「Fabric CA 用戶端」移至其中的目錄中執行此指令。實際的呼叫可能類似下列指令範例：
  ```
  ./fabric-ca-client enroll -u https://admin:dda0c53f7b@n7413e3b503174a58b112d30f3af55016-org1-ca.us3.blockchain.ibm.com:31011 --caname org1CA --tls.certfiles $HOME/tls/us2.blockchain.ibm.com.cert
  ```
  {:codeblock}

6. 在 `$FABRICCA_CLIENT_HOME/msp/signcerts/cert.pem` 中尋找您的管理憑證。然後，您可以從「網路監視器」將管理憑證上傳至區塊鏈網路。如需新增憑證的相關資訊，請參閱「網路監視器」中[「成員」畫面的「憑證」標籤](v10_dashboard.html#members)。

  您也可以在下列目錄中找到 CA 主要憑證和管理私密金鑰：
  * CA 主要憑證：`$FABRIC_CA_CLIENT_HOME/msp/cacerts/--<ca_name>.pem`
  * 管理私密金鑰：`$FABRIC_CA_CLIENT_HOME/msp/keystore/<>_sk file`

參閱您將使用「Fabric CA 用戶端」登記的範例，並使用所產生的憑證，依[操作遠端對等節點](howto/remote_peer_operate_icp.html#remote-peer-cli-operate)的指示來操作網路元件。

### 使用 Fabric CA 用戶端登錄
{: #register-app-caclient}

1. 發出下列指令，以在您的區塊鏈網路中尋找您的連結與組織名稱。
  ```
  ./fabric-ca-client affiliation list --tls.certfiles pathToPem
  ```
  {:codeblock}

  您應該會看到類似下列範例的資訊：
  ```
  affiliation: ibp
      affiliation: ibp.PeerOrg1
  ```
  {:codeblock}

  請記下第二個**連結**值，例如 `ibp.PeerOrg1`。您需要在下面的指令中使用此值。

2. 執行下列指令來登錄對等節點。
  ```
  ./fabric-ca-client register --id.name <name> --id.affiliation <affiliation> --id.secret <password> --tls.certfiles pathToPem
  ```
  {:codeblock}

  指定對等節點的名稱和密碼，並將 `name` 和 `password` 取代為對等節點名稱和密碼。記下此資訊。當您配置對等節點時，需要它。例如：
  ```
  ./fabric-ca-client register --id.name user1 --id.affiliation ibp.PeerOrg1 --id.secret userpw  --tls.certfiles --tls.certfiles $HOME/tls/us2.blockchain.ibm.com.cert
  ```
  {:codeblock}

  您只能登錄一次身分。如果您遇到問題，請嘗試使用新的使用者名稱和密碼來嘗試指令。

  當指令順利完成時，您應該會看到類似下列範例的資訊：
  ```
  2018/06/18 16:53:00 [INFO] Configuration file location: /fabric-ca-platform/admin/fabric-ca-client-config.yaml
  2018/06/18 16:53:00 [INFO] TLS Enabled
  2018/06/18 16:53:00 [INFO] TLS Enabled
  Password: userpw
  ```
  {:codeblock}
