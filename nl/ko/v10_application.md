---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 애플리케이션 개발
{: #dev_app}
애플리케이션을 사용하여 블록체인 네트워크에서 채널 특정 원장을 조회하거나 업데이트하기 위해 체인코드를 호출할 수 있습니다.
{:shortdesc}

## 애플리케이션 개발 환경 설정
{{site.data.keyword.cloud}}에서 블록체인 네트워크와 상호작용할 수 있는 애플리케이션을 개발하기 위한 필수 소프트웨어를 설치해야 합니다.
{:shortdesc}

*	Git([Git 다운로드 페이지 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://git-scm.com/downloads){:new_window})  
	Git는 일반적으로 체인코드 개발 및 소프트웨어 개발에 모두 친숙해지도록 하기 위한 버전 제어 도구입니다. 또한, Windows에서 git와 함께 설치되는 git bash는 Windows 명령 프롬프트에 대한 탁월한 대체품입니다.

*	GoLang([GoLang 다운로드 페이지 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://golang.org/dl){:new_window})  
	GoLang 설치는 Go CLI 도구 세트를 설치하며, 이는 체인코드를 작성하는 데 매우 유용합니다. 예를 들어, `go build` 명령을 사용하면 체인코드를 네트워크에 배치하기 전에 실제로 컴파일하는지 확인할 수 있습니다.

	환경 변수를 올바르게 설정하려면 [설치 지시사항 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://golang.org/doc/install){:new_window}을 따르십시오. 아래 명령을 사용하여 `GOPATH`를 확인하십시오. `GOPATH`는 예제와 일치하지 않아도 됩니다. 사용자의 파일 시스템에서 올바른 디렉토리에 이 변수가 설정되어 있다는 것만이 중요합니다.

	```
	$ echo $GOPATH
	C:\gopath
	```
	{:codeblock}

	그리고 나서 [hello world ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://golang.org/doc/install#testing){:new_window} 예제를 사용하여 GoLang 코드를 빌드하여 GoLang 설치를 확인할 수 있습니다.

* Java([Java 다운로드 페이지 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://java.com/en/download/){:new_window}).
*	Node.js([Node.js 다운로드 페이지 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://nodejs.org/en/download/){:new_window}).

체인코드 개발은 현재 Node.js, Go 및 Java에서 지원됩니다.

## 클라이언트 측 인증서 생성
x509 및 공개 키 인프라의 세부사항을 깊게 조사하지는 않으며, 이에 대한 외부 리소스가 많이 있습니다. Fabric의 통신 플로우가 모든 터치포인트에서 서명/확인 오퍼레이션을 사용합니다. 이와 같이 네트워크에 호출(즉, 원장 조회 또는 업데이트)을 전송하는 클라이언트는 페이로드에 서명해야 하며 확인 목적으로 올바르게 서명된 x509 인증서를 첨부해야 합니다. 개인 키 및 서명된 인증서는 MSP ID 및 인증 기관(CA) 루트 인증서와 함께 "사용자 컨텍스트" 오브젝트라고도 하는 항목을 구성합니다.

여기서 중요한 것은 오브젝트 형성을 허용하는 키 및 인증서가 적합한 CA에서 검색되는 "등록접수(enrollment)"라는 프로세스입니다. 사용자 컨텍스트 오브젝트를 형성한 후에는 이 사용자 컨텍스트를 "설정"하거나 "가져오기" 위해 애플리케이션에서 API를 호출할 수 있습니다. 이 지점에서 애플리케이션(예: 클라이언트)은 필요한 모든 아티팩트 설비를 갖추고 네트워크와 통신할 준비가 됩니다. 키와 인증서를 검색하기 위한 두 가지 접근방식(명령행과 SDK)을 살펴볼 것입니다.

### 명령행
명령행 사용은 두 가지 접근방식 중 더 단순한 방식입니다.

1. 지시사항을 따라서 [Fabric CA 클라이언트 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://hyperledger-fabric-ca.readthedocs.io/en/latest/users-guide.html)를 빌드하십시오. 이 단계를 통해 사용자가 CA 서버와 통신하고 올바르게 형식화된 인증서와 키를 수신할 수 있습니다.

2. 사용하는 서비스 플랜, 위치 및 클러스터에 따라 {{site.data.keyword.cloud_notm}}에서 TLS 인증서를 다운로드하십시오.
  - 스타터 플랜의 루트 TLS 인증서  
    - 미국: [us01.blockchain.ibm.com.cert ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://blockchain-certs.mybluemix.net/us01.blockchain.ibm.com.cert "us01.blockchain.ibm.com.cert"), [us02.blockchain.ibm.com.cert ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://blockchain-certs.mybluemix.net/us02.blockchain.ibm.com.cert "us02.blockchain.ibm.com.cert")
    - 영국: [uk01.blockchain.ibm.com.cert ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://blockchain-certs.mybluemix.net/uk01.blockchain.ibm.com.cert "uk01.blockchain.ibm.com.cert"), [uk02.blockchain.ibm.com.cert ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://blockchain-certs.mybluemix.net/uk02.blockchain.ibm.com.cert "uk02.blockchain.ibm.com.cert")
    - 시드니: [aus01.blockchain.ibm.com.cert ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://blockchain-certs.mybluemix.net/aus01.blockchain.ibm.com.cert "aus01.blockchain.ibm.com.cert"), [aus02.blockchain.ibm.com.cert ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://blockchain-certs.mybluemix.net/aus02.blockchain.ibm.com.cert "aus02.blockchain.ibm.com.cert")
  - [엔터프라이즈 플랜에 대한 루트 TLS 인증서 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://blockchain-certs.mybluemix.net/3.secure.blockchain.ibm.com.rootcert)

  컨텐츠를 폴더(예: ``$HOME/tls``)에 저장하십시오. 이 단계는 데이터 플로우가 연결에서 암호화되도록 허용합니다.

3. 네트워크 모니터의 **개요** 화면에서 **연결 프로파일** JSON 파일을 열고 다음 변수를 찾으십시오.
  * CA의 URL: ``certificateAuthorities`` 아래 ``url``
  * 관리자 ID: ``enrollId``
  * 관리 비밀번호: ``enrollSecret``
  * CA 이름: ``caName``

4. Fabric CA 클라이언트를 사용하면 TLS 인증서 경로 및 위의 네 개 문자열을 다음 명령과 함께 전달하여 인증 기관에 "등록접수" 호출을 전송할 수 있습니다.
  ```
$GOPATH/bin/fabric-ca-client enroll -u https://<enroll_id>:<enroll_password>@<ca_url_with_port> --caname <ca_name> --tls.certfiles <tls_cert_path>
  ```
  {:codeblock}

  ``fabric-ca-client`` 바이너리는 ``$GOPATH/bin``에 위치하므로 이 명령을 실행할 때는 사용자가 로컬 시스템의 올바른 위치에 있어야 합니다.  실제 호출은 다음 예제 명령과 비슷하게 보일 수 있습니다.
  ```
./fabric-ca-client enroll -u https://admin:B84F2C5436@tor-zbc01a.3.secure.blockchain.ibm.com:23042 --tls.certfiles /Users/XYZ/Downloads/3.secure.blockchain.ibm.com.rootcert --caname PeerOrg1CA
  ```
  {:codeblock}

5. `$HOME/.fabric-ca-client/msp/signcerts/cert.pem`에서 관리자 인증서를 찾으십시오. 그런 다음 네트워크 모니터에서 사용자의 블록체인 네트워크에 관리자 인증서를 업로드할 수 있습니다. 인증서 추가에 대한 자세한 정보는 네트워크 모니터에서 ["구성원" 화면의 "인증서" 탭](v10_dashboard.html#members)을 참조하십시오.

  또한, CA 루트 인증서 및 관리자 개인 키를 다음 디렉토리에서 찾을 수 있습니다.
  * CA 루트 인증서: `$HOME/.fabric-ca-client/msp/cacerts/--<ca_name>.pem`
  * 관리자 개인 키: `$HOME/.fabric-ca-client/msp/keystore/<>_sk file`

### SDK
인증 기관과 프로그래밍 방식으로 상호작용하는 방법을 이해하기 위한 우수한 리소스 및 스크립트가 포함된 두 개의 Fabric 저장소가 있습니다. ``fabric-samples`` 저장소에는 ``balance transfer`` 예제가 포함되어 있으며 ``fabric-sdk-node`` 저장소에는 일련의 CA 서비스 테스트가 있습니다. 애플리케이션 측에서 등록접수 요청을 발행하려는 경우에는 ``fabric-ca-client`` 및 ``fabric-client`` 패키지 내에서 노출해야 하는 API를 완전하게 이해해야 합니다. 앱 구조화를 위한 기준선으로서의 이러한 스크립트 및 저장소를 사용하십시오.

`balance transfer` 예제의 몇 가지 주요 스니펫을 빠르게 살펴보겠습니다.

우선 클라이언트 오브젝트를 작성하고 인증서와 키가 일시 보관될 키-값 저장소 인스턴스를 설정해야 합니다. ``BaseClient``에서 ``Client`` 클래스로 확장하는 단순한 팩토리 메소드(``newCryptoSuite``)로 이를 수행할 수 있습니다. 여기서는 다음 코드를 간단히 살펴보겠습니다.

```
# <PUBLIC_PRIVATE_KEY_PATH> denotes the path on your local machine where you wish to store your key and cert
let cryptoSuite = hfc.newCryptoSuite();
cryptoSuite.setCryptoKeyStore(hfc.newCryptoKeyStore({path: <PUBLIC_PRIVATE_KEY_PATH>)}));
client.setCryptoSuite(cryptoSuite);
```
{:codeblock}

사용자의 시스템에서 키/값 경로를 정의하는 환경 변수를 내보내고 이를 위의 함수에 전달하는 것이 공통 사례입니다. 이제 KVS를 정의했으므로 ``FabricCAServices`` 클래스에서 몇 개의 메소드를 사용하도록 합니다. 이 클래스는 Fabric CA 클라이언트의 구현이며, 그와 같이 우리가 CA 서버와 통신하도록 허용합니다. 우선 CA 클라이언트, 즉 CA URL에 일부 정보를 전달해야 합니다.

```
# the caURL can be defined manually or by setting an environment variable
# the copService variable is defined at the top of the program 
let caUrl = "https://XXX:7054";
var caClient = new copService(caUrl, null, '' /* default CA */, cryptoSuite);
```
{:codeblock}

그 다음에 "등록접수" 호출을 CA 서버에 실제로 전송하게 됩니다. 이렇게 하면 x509 인증서에 랩핑되고 대상 지정된 CA에서 서명한 개인 키 및 공개 키가 클라이언트로 리턴되며, 이를 서명인증 또는 등록접수 인증서라고 합니다. 네트워크 엔티티가 클라이언트에서 시작하는 호출 및 트랜잭션을 확인하도록 허용하기 때문에 이 등록접수 인증서 즉 "eCert"는 키 조각입니다.

```
return caClient.enroll({
enrollmentID: username,
enrollmentSecret: password
```
{:codeblock}

그리고 마지막 태스크는 암호 스위트를 실제로 설정하고 사용자 컨텍스트를 빌드하는 것입니다.

```
	member.setCryptoSuite(client.getCryptoSuite());
	return member.setEnrollment(enrollment.key, enrollment.certificate, getMspID(userOrg));
}).then(() => {
	return client.setUserContext(member);
```
{:codeblock}

그런 다음 네트워크 모니터에서 사용자의 블록체인 네트워크에 관리자 인증서를 업로드할 수 있습니다. 인증서 추가에 대한 자세한 정보는 네트워크 모니터에서 ["구성원" 화면의 "인증서" 탭](v10_dashboard.html#members)을 참조하십시오.

## 애플리케이션 개발
{: #developing-applications}

애플리케이션 개발을 시작하는 쉬운 방법은 샘플 체인코드 및 애플리케이션을 사용자 고유의 비즈니스 솔루션 작성을 위한 템플리트로 사용하는 것입니다. [샘플 애플리케이션](howto/prebuilt_samples.html)에서 {{site.data.keyword.cloud_notm}}의 블록체인 네트워크에 대한 샘플 애플리케이션을 찾을 수 있습니다. 사용자 고유의 비즈니스 요구사항에 따라 애플리케이션 개발을 처음부터 시작할 수도 있습니다.

JavaScript 또는 Java로 애플리케이션을 개발하고 Hyperledger Fabric Client SDK에서 사용 가능한 API를 활용하여 애플리케이션과 네트워크 간에 상호작용이 가능하게 할 수 있습니다.  애플리케이션에는 최소한 다음 정보가 포함되어야 합니다.
* 호출할 체인코드의 이름 및 버전.
* 순서 지정자, CA 및 피어를 포함하는 네트워크 리소스의 API 엔드포인트 정보.
* 네트워크에서 원장을 조회하거나 업데이트하는 기능.  고가용성을 원하는 경우, 사용자의 애플리케이션에서 노드 장애 복구를 고려해야 합니다.

### Fabric SDK 사용
{: #use-sdks}

Fabric은 현재 Node.js SDK 및 Java SDK를 제공하고 향후 릴리스에서 Python, REST 또는 GO와 같은 추가 프로그래밍 언어를 지원합니다. Fabric SDK 및 사용 방법에 대한 자세한 정보는 다음 문서를 참조하십시오.

- [Hyperledger Fabric 노드 SDK 문서 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://fabric-sdk-node.github.io/){:new_window}
- [Hyperledger Fabric Java SDK 문서 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://github.com/hyperledger/fabric-sdk-java){:new_window}

### Fabric SDK에서 제한시간 값 설정
{: #set-timeout-in-sdk}

Fabric SDK는 블록체인 네트워크의 이벤트에 대한 클라이언트 애플리케이션의 기본 제한시간 값을 설정합니다. Fabric Java SDK의 기본 제한시간 설정에 대한 다음 예제를 참조하십시오. 파일 경로는 `src\main\java\org\hyperledger\fabric\sdk\helper\Config.java`입니다.

```
    /**
     * Timeout settings
     **/
    public static final String PROPOSAL_WAIT_TIME = "org.hyperledger.fabric.sdk.proposal.wait.time";
    public static final String CHANNEL_CONFIG_WAIT_TIME = "org.hyperledger.fabric.sdk.channelconfig.wait_time";
    public static final String TRANSACTION_CLEANUP_UP_TIMEOUT_WAIT_TIME = "org.hyperledger.fabric.sdk.client.transaction_cleanup_up_timeout_wait_time";
    public static final String ORDERER_RETRY_WAIT_TIME = "org.hyperledger.fabric.sdk.orderer_retry.wait_time";
    public static final String ORDERER_WAIT_TIME = "org.hyperledger.fabric.sdk.orderer.ordererWaitTimeMilliSecs";
    public static final String PEER_EVENT_REGISTRATION_WAIT_TIME = "org.hyperledger.fabric.sdk.peer.eventRegistration.wait_time";
    public static final String PEER_EVENT_RETRY_WAIT_TIME = "org.hyperledger.fabric.sdk.peer.retry_wait_time";
    public static final String EVENTHUB_CONNECTION_WAIT_TIME = "org.hyperledger.fabric.sdk.eventhub_connection.wait_time";
    public static final String EVENTHUB_RECONNECTION_WARNING_RATE = "org.hyperledger.fabric.sdk.eventhub.reconnection_warning_rate";
    public static final String PEER_EVENT_RECONNECTION_WARNING_RATE = "org.hyperledger.fabric.sdk.peer.reconnection_warning_rate";
    public static final String GENESISBLOCK_WAIT_TIME = "org.hyperledger.fabric.sdk.channel.genesisblock_wait_time";

    ...

    // Default values
    /**
     * Timeout settings
     **/
    defaultProperty(PROPOSAL_WAIT_TIME, "20000");
    defaultProperty(CHANNEL_CONFIG_WAIT_TIME, "15000");
    defaultProperty(ORDERER_RETRY_WAIT_TIME, "200");
    defaultProperty(ORDERER_WAIT_TIME, "10000");
    defaultProperty(PEER_EVENT_REGISTRATION_WAIT_TIME, "5000");
    defaultProperty(PEER_EVENT_RETRY_WAIT_TIME, "500");
    defaultProperty(EVENTHUB_CONNECTION_WAIT_TIME, "5000");
    defaultProperty(GENESISBLOCK_WAIT_TIME, "5000");
    /**
     * This will NOT complete any transaction futures time out and must be kept WELL above any expected future timeout
     * for transactions sent to the Orderer. For internal cleanup only.
     */
    defaultProperty(TRANSACTION_CLEANUP_UP_TIMEOUT_WAIT_TIME, "600000"); //10 min.
```
{:codeblock}

그러나 사용자 고유의 애플리케이션에서 기본 제한시간 값을 변경해야 할 수 있습니다. 예를 들어, 애플리케이션이 이벤트 허브 연결의 기본 제한시간 값인 5000밀리초보다 응답하는 데 더 오랜 시간이 필요한 트랜잭션을 호출하는 경우 트랜잭션이 완료되기 전에 호출 이벤트가 5000밀리초에 종료되므로 실패 오류가 발생합니다. 클라이언트 애플리케이션의 기본값을 겹쳐쓰도록 시스템 특성을 설정할 수 있습니다. 시스템 특성을 설정하기 전에 기본값이 초기화되므로 시스템 특성이 적용되지 않을 수 있습니다. 따라서 클라이언트 애플리케이션에서 제한시간에 대한 시스템 특성을 정적 구조체에 설정해야 합니다. Fabric Java SDK에서 이벤트 허브 연결의 제한시간 값을 15000밀리초로 변경하는 데 대한 다음 예제를 참조하십시오. 파일 경로는 `src\main\java\org\hyperledger\fabric\sdk\helper\Config.java`입니다.

```
 public static final String EVENTHUB_CONNECTION_WAIT_TIME = "org.hyperledger.fabric.sdk.eventhub_connection.wait_time";
 private static final long EVENTHUB_CONNECTION_WAIT_TIME_VALUE = 15000;

 static {
     System.setProperty(EVENTHUB_CONNECTION_WAIT_TIME, EVENTHUB_CONNECTION_WAIT_TIME_VALUE);
 }
```
{:codeblock}


## 애플리케이션에 네트워크 API 엔드포인트 추가
{{site.data.keyword.Bluemix_short}}에서 {{site.data.keyword.blockchain}} 네트워트와 상호작용할 수 있도록 네트워크 리소스의 API 엔드포인트를 애플리케이션에 추가해야 합니다.  {{site.data.keyword.Bluemix_short}}에 {{site.data.keyword.blockchain}} 네트워크가 없는 경우 스타터 플랜 또는 엔터프라이즈 플랜에서 작성할 수 있습니다. 자세한 정보는 [스타터 플랜 네트워크 통제](get_start_starter_plan.html) 및 [엔터프라이즈 플랜 네트워크 통제](get_start.html)를 참조하십시오.

네트워크의 연결 프로파일에서 API 엔드포인트를 찾을 수 있습니다. 연결 프로파일은 JSON 형식이며 API 엔드포인트 정보 및 순서 지정자, CA, 피어 노드를 포함하는 네트워크 리소스의 enrollID/시크릿을 포함합니다. 사용자의 애플리케이션은 이러한 API 엔드포인트를 통해 피어 및 기타 네트워크 리소스와 상호작용합니다.

1. 다음 방법 중 하나로 네트워크 모니터에서 네트워크 리소스의 API 엔드포인트 정보를 검색하십시오.
	* 체인코드 특정 API 엔드포인트 정보를 가져오려면 체인코드가 실행 중인 특정 채널 화면에서 체인코드를 찾아서 **JSON** 단추를 클릭하십시오.
	![체인코드별 API 엔드포인트](images/channel_chaincode.png "체인코드별 API 엔드포인트")
	* 모든 네트워크 리소스에 대한 API 엔드포인트 정보의 전체 세트를 가져오려면 "개요" 화면에서 **연결 프로파일** 단추를 클릭하십시오.
	![네트워크 모니터의 연결 프로파일](images/service_credentials.png "네트워크 모니터의 연결 프로파일")

2. 네트워크 리소스의 API 엔드포인트 정보를 찾으십시오. 다음 예제와 유사합니다.
	```
	"peers": {
            "fabric-peer-org3-18400c": {
                "url": "grpcs://tor-zbc06c.3.secure.blockchain.ibm.com:18400",
                "eventUrl": "grpcs://tor-zbc06c.3.secure.blockchain.ibm.com:13547",
                ...
	```
	{:codeblock}
	**참고**: 예를 들어 네트워크에서 추가 피어를 대상으로 지정하려는 경우, 사용자의 조직에 속하지 않는 피어에서 보증이 필요하며, 그 다음에 해당 피어 중에서 올바른 API 엔드포인트 정보를 획득해야 합니다.  애플리케이션에 리턴되는 응답을 확인하기 위해 다른 조직에 대한 CA 인증서를 저장해야 할 수도 있습니다. 이 정보는 연결 프로파일에 노출되지 않으므로, Cloud Foundry 조직의 적합한 관리자에게 문의하여 대역 외 오퍼레이션에서 이 정보를 획득해야 합니다. 순서 지정 서비스 URL은 네트워크에서 공통이므로 순서 지정 서비스에 대한 구성원 특정 정보가 필요하지 않습니다.

3. 다음 예제에 표시된 대로 API 엔드포인트 정보를 애플리케이션의 구성 파일에 플러그로 지정하십시오.
	```
	orderer_url: 'grpcs://fft-zbc01a.4.secure.blockchain.ibm.com:18603'
	```
	{:codeblock}

## CouchDB 인덱스

네트워크에서 CouchDB를 사용하는 경우 CouchDB의 성능을 향상시키는 CouchDB 인덱싱 기능을 활용하려면 인덱스가 체인코드와 함께 패키징되어야 합니다.

CouchDB 및 인덱스를 설정하는 방법에 대해 자세히 알아보려면 [CouchDB에 대한 Fabric 문서 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](http://hyperledger-fabric.readthedocs.io/en/release-1.1/couchdb_as_state_database.html)를 참조하십시오.

## 애플리케이션 호스팅
로컬 파일 시스템에 애플리케이션을 호스팅하거나 {{site.data.keyword.Bluemix_notm}}에 푸시할 수 있습니다. 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하려면 다음 단계를 완료하십시오.
1. [Cloud Foundry 명령행 설치 프로그램 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/cli/releases)을 설치하십시오.  `cf` 명령으로 설치를 테스트하십시오.
    * 설치가 완료되면 사용자의 터미널에 다수의 텍스트 출력이 표시되어야 합니다.
    * "명령을 찾을 수 없음"이 표시되면 설치에 성공하지 못했거나 CF가 사용자의 시스템 경로에 추가되지 않은 것입니다.
2. API 엔드포인트를 설정하고 다음 명령을 실행하여 {{site.data.keyword.Bluemix_notm}} ID 및 비밀번호로 로그인하십시오.
    ```
    > cf api https://api.ng.bluemix.net
    > cf login
    ```
    {:codeblock}
3. 애플리케이션의 디렉토리를 찾아서 다음 명령을 실행하여 애플리케이션을 푸시하십시오. 이는 사용자의 애플리케이션 크기에 따라 몇 분이 소요될 수 있습니다. {{site.data.keyword.Bluemix_notm}}의 로그가 사용자의 터미널에 표시되며, 애플리케이션이 실행되면 중단됩니다.
	```
	> cf push YOUR_APP_NAME_HERE
	```
	{:codeblock}
	다음 명령 중 하나를 실행하여 애플리케이션 로그를 확인할 수 있습니다.
	* `> cf logs YOUR_APP_NAME_HERE`
	* `> cf logs YOUR_APP_NAME_HERE --recent`


## 네트워크에서 애플리케이션 연결 끊기
{: #disconnect}
사용자의 애플리케이션과 {{site.data.keyword.Bluemix_short}}에서 {{site.data.keyword.blockchain}} 네트워크 사이의 연결을 제거하려면 다음 단계를 완료하십시오.
1. 애플리케이션 구성 파일에서 API 엔드포인트 정보를 제거하십시오. 참조사항은 [애플리케이션에 네트워크 API 엔드포인트 추가](#adding-network-api-endpoints-to-your-application)를 참조하십시오.
2. 체인코드 컨테이너를 삭제하십시오.
	1. 네트워크 모니터의 "채널" 화면에서 체인코드가 설치된 채널을 찾으십시오.
	2. 특정 채널 화면에서 사용 안함으로 설정하려는 체인 코드를 찾으십시오.
	3. **삭제** 단추를 클릭하고 체인코드 삭제 패널에서 **제출**을 클릭하십시오. 체인코드 컨테이너가 제거됩니다.
	![체인코드 삭제](images/channel_chaincode.png "체인코드 삭제")
