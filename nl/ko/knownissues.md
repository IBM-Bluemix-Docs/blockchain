---

copyright:
  years: 2017, 2019

lastupdated: "2019-06-18"

subcollection: blockchain

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}

# 알려진 문제
{: #known-issues}

이 페이지에서는 스타터 또는 엔터프라이즈 플랜을 사용할 때 발생할 수 있는 알려진 문제에 대해 설명합니다.
{:shortdesc}

다음 문제가 이미 보고되었습니다.
- **외부 CA 구성은 아직 지원되지 않습니다**. 그 대안으로 네트워크 모니터를 통해 관리자 인증서를 생성해서 업로드할 수 있습니다. 자세한 정보는 네트워크 모니터에서 ["구성원" 화면의 "인증서" 탭](/docs/services/blockchain/v10_dashboard.html#ibp-dashboard-members)에 대한 설명을 참조하십시오. 
- 스타터 플랜 네트워크의 네트워크 모니터에서 "개요" 화면에 나열된 노드에 대해 **로그 보기**를 클릭하면 {{site.data.keyword.cloud}} 로깅 Kibana 인터페이스가 열립니다. **기본적으로 Kibana는 최근 30일 동안의 활동에 대한 로그를 표시하도록 사전 구성됩니다**. 최근 30일 동안 활동이 없으면 *결과를 찾을 수 없음*이라는 메시지가 표시됩니다. 다른 로그를 보려면 오른쪽 상단 모서리에 있는 사용자 이름 아래의 타이머 아이콘을 클릭하고 광범위한 시간 범위(예: *연간 누계*)를 설정할 수 있습니다.
- 스타터 플랜 네트워크의 로그는 [{{site.data.keyword.cloud_notm}} 로그 분석 서비스](https://cloud.ibm.com/catalog/services/log-analysis){: external}를 통해 수집됩니다. 기본적으로 로그는 로그 분석 서비스의 Lite 플랜에서 수집됩니다. 이 플랜은 무료이며 **매일 처음 500MB의 로그만 검색할 수 있도록 허용합니다**. 네트워크의 로그가 500MB를 초과하면 Kibana에서 새 로그를 볼 수 없습니다. 네트워크가 500MB를 넘는 로그를 생성하는 경우 로그 분석 서비스의 유료 버전으로 업그레이드할 수 있습니다.
- 스타터 플랜은 프로덕션 환경이 아니므로 **애플리케이션이 바로 네트워크 리소스에 도달할 수 없을 수도 있습니다**.
  - 이러한 상황이 발생하면 첫 번째 단계로 Fabric SDK에서 기본 제한시간 값을 늘리는 것이 권장됩니다. 제한시간 값 설정에 대한 자세한 정보는 [Fabric SDK에서 제한시간 값 설정](/docs/services/blockchain/best_practices.html#best-practices-app-set-timeout-in-sdk)을 참조하십시오.
  - 또한 애플리케이션 레벨에서 요청을 재시도할 수 있습니다.
- 백그라운드 네트워크 문제로 인해 **체인코드 컨테이너가 때때로 중지될 수 있으며** 사용자가 체인코드를 호출한 후 다시 빌드되고 다시 시작되어야 할 수 있습니다. 이러한 상황이 발생하면 체인코드 응답에 수 분이 걸릴 수 있습니다.
- 스타터 플랜 네트워크의 리소스 제한사항(즉, 피어당 1개의 CPU 및 4Gi RAM)으로 인해 **체인코드 설치 중에 `REQUEST_TIMEOUT` 오류가 발생할 수 있습니다**. 이러한 상황이 발생하면 설치 단계를 재시도하십시오. 오류가 계속되면 체인코드 설치 제한시간을 늘릴 수 있습니다. 연결 프로파일에서 체인코드 설치 제한시간은 300초로 설정됩니다.
  - SDK에서 기본 제한시간 값을 사용하는 경우 아래에 표시된 대로(제한시간을 300초로 설정) 연결 프로파일에서 **클라이언트** 섹션을 복사하고 SDK가 이를 읽도록 하십시오. 노드 SDK의 경우 연결 프로파일의 이 제한시간 설정은 모든 호출(예: `invoke`, `queries`)에 적용됩니다.
    ```
    "client": {
       "organization": "Org1",
       "connection": {
           "timeout": {
               "peer": {
                   "endorser": "300"
               }
           }
       }
    },
    ```
    {:codeblock}
  - SDK에서 체인코드 설치 명령의 제한시간 설정을 겹쳐쓰는 경우 이를 다시 기본값으로 설정하거나 300초 이상으로 변경하십시오.
    - 노드 SDK를 사용하는 경우 `sendInstantiateProposal(request, timeout)` 메소드의 제한시간 설정을 변경할 수 있습니다. 자세한 정보는 [sendInstantiateProposal(request, timeout)](https://fabric-sdk-node.github.io/Channel.html#sendInstantiateProposal){: external}을 참조하십시오. 
    - Java SDK를 사용하는 경우 `src/test/java/org/hyperledger/fabric/sdkintegration/End2endIT.java` 파일에 있는 `instantiateProposalRequest.setProposalWaitTime(DEPLOYWAITTIME)` 명령의 제한시간 설정을 변경할 수 있습니다.

{{site.data.keyword.cloud_notm}}의 {{site.data.keyword.blockchainfull_notm}} Platform 네트워크에 대한 지원 및 도움은 [지원 받기](/docs/services/blockchain/ibmblockchain_support.html#blockchain-support)를 참조하십시오.
