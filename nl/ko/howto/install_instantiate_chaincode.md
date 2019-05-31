---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-16"

keywords: chaincode endorsement policy, install chaincode, instantiate chaincode, update chaincode

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 체인코드 설치, 인스턴스화 및 업데이트
{: #install-instantiate-chaincode}


체인코드는 원장의 자산 작성 및 수정을 위한 비즈니스 로직 및 트랜잭션 명령어를 캡슐화하는 소프트웨어입니다. 체인코드는 여러 다른 언어로 쓸 수 있으며 {{site.data.keyword.blockchainfull}} Platform에서는 Go와 Node.js 체인코드를 지원합니다. 체인코드는 상호작용해야 하는 피어와 연관된 Docker 컨테이너에서 실행됩니다. 체인코드 개발에 대한 자세한 정보는 [체인코드 튜토리얼 ![외부 링크 아이콘](../images/external_link.svg "외부 링크 아이콘")](https://hyperledger-fabric.readthedocs.io/en/release-1.2/chaincode.html)을 참조하십시오.
{:shortdesc}

체인코드가 피어에 설치된 다음 채널에서 인스턴스화됩니다. **체인코드를 사용하여 트랜잭션을 제출하거나 데이터를 읽으려는 모든 구성원은 피어에 체인코드를 설치해야 합니다.** 체인코드는 해당 이름과 버전으로 정의됩니다. 설치된 체인코드의 이름과 버전은 채널의 전체 피어에서 일관되어야 합니다.

체인코드를 피어에 설치하고 나면 단일 네트워크 구성원이 채널에서 체인코드를 인스턴스화합니다. 이 조치를 수행하려면 네트워크 구성원이 채널에 가입해야 합니다. 인스턴스화는 체인코드에서 사용하는 초기 데이터를 입력한 다음 체인코드가 설치된 채널에 가입하는 피어에서 체인코드 컨테이너를 시작합니다. 그런 다음 피어에서는 실행 컨테이너를 사용하여 트랜잭션을 수행할 수 있습니다. **하나의 네트워크 구성원만 체인코드를 인스턴스화하면 됩니다.** 체인코드가 설치된 피어가 이미 인스턴스화된 채널에 가입하면 체인코드 컨테이너가 자동으로 시작됩니다.

**설치 및 인스턴스화** 조합을 사용하면 피어가 여러 채널에서 단일 체인코드를 사용할 수 있으므로 강력한 기능이 됩니다. 피어에서 동일한 체인코드를 사용하지만 데이터에 액세스할 수 있는 여러 다른 네트워크 구성원 세트가 있는 여러 채널에 가입하려 할 수 있습니다. 피어에서 체인코드를 한 번 설치한 다음, 인스턴스화된 임의 채널에서 동일한 체인코드 컨테이너를 사용할 수 있습니다. 이 경량 접근법을 사용하면 계산 및 스토리지 공간을 절약하고 네트워크를 확장하는 데 도움이 됩니다.

## 체인코드 설치
{: #install-instantiate-chaincode-install-cc}

이 체인코드를 실행할 모든 피어에 체인코드를 설치해야 합니다. 체인코드를 설치하려면 다음 단계를 완료하십시오.
1. 네트워크 모니터의 "코드 설치" 화면에 있는 드롭 다운 목록에서 체인코드를 설치할 피어를 선택하십시오. **체인코드 설치** 단추를 클릭하십시오.
<!--
  ![Chaincode screen](../images/chaincode_install_overview.png "Chaincode screen")
-->

2. **체인코드 설치** 팝업 패널에서 체인코드의 이름과 버전을 입력하십시오. 설치된 체인코드와 상호작용할 애플리케이션에서 이름 및 버전 문자열이 사용된다는 점을 **참고**하십시오. **찾아보기** 단추를 클릭하고 체인코드 소스 파일이 저장되는 로컬 파일 시스템으로 이동하십시오. 피어에 설치할 하나 이상의 체인코드 소스 파일을 선택하십시오. 그런 다음 **체인코드 유형** 드롭 다운에서 체인코드 언어를 선택하십시오.

단일 또는 다중 GO 또는 NODE 파일을 업로드하여 체인코드를 설치하거나 .zip 파일 내에 체인코드를 업로드할 수 있습니다. .zip 파일 사용 시 완전한 디렉토리 구조로 체인코드를 유지보수합니다. 이는 종속 항목 패키지를 포함하거나 CouchDB에서 인덱스를 사용하려는 경우에 유용합니다. CouchDB에 관한 자세한 정보와 인덱스 설정 방법은 애플리케이션 개발 튜토리얼의 [CouchDB 사용 시의 우수 사례](/docs/services/blockchain/best_practices.html#best-practices-app-couchdb-indices)를 참조하십시오. Hyperledger Fabric 문서의 [Go로 작성된 체인코드의 외부 종속 항목 관리 ![외부 링크 아이콘](../images/external_link.svg "외부 링크 아이콘")](https://hyperledger-fabric.readthedocs.io/en/release-1.2/chaincode4ade.html#managing-external-dependencies-for-chaincode-written-in-go){:new_window}에서 정보를 찾을 수도 있습니다.

  ![체인코드 설치](../images/chaincode_install.png "체인코드 설치")

## 체인코드 인스턴스화
{: #install-instantiate-chaincode-instantiate-cc}


채널에 가입하는 모든 피어의 파일 시스템에 체인코드를 설치한 후에는 체인코드를 채널에서 인스턴스화해야 피어가 체인코드 컨테이너를 통해 원장과 상호작용할 수 있습니다. 인스턴스화는 체인코드의 초기화가 필요한 경우 이를 수행합니다. 종종 체인코드의 초기 세계 상태를 구성하는 키 값 쌍 설정이 포함됩니다.

체인코드를 인스턴스화하려면 채널에 **운영자** 또는 **작성자** 권한이 있어야 합니다. 다른 피어에서 이름과 버전이 같은 체인코드를 체인코드 컨테이너에 배치하려면 한 번만 인스턴스화해야 합니다. 체인코드를 인스턴스화하려면 다음 단계를 완료하십시오.
1. 네트워크 모니터의 "코드 설치" 화면에서 체인코드를 설치한 피어를 선택하고 체인코드 테이블에서 인스턴스화할 체인코드를 찾으십시오. 그런 다음 **조치** 헤더 아래에서 **인스턴스화** 단추를 클릭하십시오.
<!--
  ![Instantiate Chaincode](../images/chaincode_instantiate.png "Instantiate Chaincode")
-->

2. **체인코드 인스턴스화** 팝업 패널에서 체인코드 초기화를 위한 인수로 키 값 쌍을 설정하고 인스턴스화할 채널을 선택하십시오.  **다음**을 클릭하십시오.
<!--
  ![Instantiate Chaincode panel](../images/chaincode_instantiate_panel.png "Instantiate Chaincode panel")
-->

3. 체인코드의 [보증 정책](/docs/services/blockchain/glossary.html#glossary-endorsement-policy)을 지정하십시오. [다음 절](#install-instantiate-chaincode-endorsement-policy)에서 보증 정책을 설정하는 방법에 대해 자세히 알아볼 수 있습니다.


## 체인코드 보증 정책 지정
{: #install-instantiate-chaincode-endorsement-policy}

보증 정책을 사용하여 새 트랜잭션을 유효성 검증해야 하는 피어 세트를 지정할 수 있습니다. 예를 들어, 보증 정책은 채널의 대다수의 구성원이 트랜잭션을 보증하는 경우에만 트랜잭션이 원장에 추가되도록 지정할 수 있습니다.

보증 정책은 체인코드가 채널에서 인스턴스화될 때 설정됩니다. 체인코드를 인스턴스화하는 조직은 체인코드를 설치한 채널 구성원 중에서 유효성 검증자가 될 구성원을 선택할 수 있으며, 모든 채널 구성원에 대한 보증 정책을 설정합니다. [체인코드 업데이트](/docs/services/blockchain/howto/install_instantiate_chaincode.html#install-instantiate-chaincode-update-cc)의 단계를 수행한 다음 두 번째 단계에서 체인코드를 다시 인스턴스화할 때 새 정책을 지정하여 보증 정책을 업데이트할 수 있습니다.

네트워크 모니터를 사용하여 보증 정책을 설정할 때 UI를 사용하여 **단순 정책**을 지정하거나 JSON을 사용하여 **고급 정책**을 지정할 수 있습니다.

* **UI를 사용하여 단순 정책 지정:** 먼저 **구성원 추가** 단추를 클릭하여 트랜잭션을 유효성 검증할 수 있는 일련의 구성원을 선택하십시오. 그런 다음 **보증 정책** 섹션에서 트랜잭션이 승인되기 전에 트랜잭션을 유효성 검증해야 하는 목록의 구성원 수를 결정하십시오. 이 방법을 사용하여 모든 채널 구성원, 이 구성원 중 대다수, 단일 구성원 또는 구성원이 자체 서명하지 못하도록 단순 +1(예: 다섯 명의 구성원 중 둘) 중 하나의 보증 정책을 지정할 수 있습니다. 변경하지 않는 경우 기본 정책에서는 채널의 임의의 구성원이 트랜잭션을 보증할 수 있습니다.

  ![단순 보증 정책](../images/simple_endorsement.png "단순 보증 정책")

* **JSON을 사용하여 고급 정책 지정:** 고급 정책을 사용하여 중요한 구성원이나 관리자의 보증을 요구하거나 특정 구성원의 보증에 가중치를 부여하십시오.

  고급 정책을 지정하는 가장 쉬운 방법은 UI 화면을 통해 단순 정책을 빌드하여 시작하는 것입니다. 그런 다음 **고급 정책** 단추를 클릭하면 정책의 JSON 버전이 단순 정책에서 설정한 경우와 동일한 구성원과 규칙으로 자동으로 채워집니다. 그런 다음 고급 버전을 작성하도록 JSON을 편집할 수 있습니다. JSON으로 보증 정책을 작성하는 방법에 대한 자세한 정보는 [Hyperledger Fabric 노드 SDK 문서![외부 링크 아이콘](../images/external_link.svg "외부 링크 아이콘")](https://fabric-sdk-node.github.io/global.html#ChaincodeInstantiateUpgradeRequest)를 참조하십시오. <!--You can also find examples of advanced endorsement policies in the main [Hyperledger Fabric documentation![External link icon](../images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/release-1.2/arch-deep-dive.html#example-endorsement-policies)-->

  ![고급 보증 정책](../images/advanced_endorsement.png "고급 보증 정책")

새 조직에서 채널에 가입하고 체인코드를 설치할 때 보증 정책은 자동으로 업데이트되지 않습니다. 예를 들어, 5개 조직 중 2개 조직에서 트랜잭션을 보증해야 하는 경우 새로운 조직에서 채널에 가입할 때 6개 조직 중 2개 조직이 필요하도록 정책이 업데이트되지 않습니다. 대신 새 조직이 정책에 나열되지 않으며 트랜잭션을 보증할 수 없습니다. 관련 체인코드를 업데이트하여 다른 조직을 보증 정책에 추가할 수 있습니다.

## 체인코드 업데이트
{: #install-instantiate-chaincode-update-cc}

원장의 자산과의 관계를 유지하면서 체인코드의 프로그래밍을 변경하도록 체인코드를 업데이트할 수 있습니다. 설치 및 인스턴스화 조합으로 인해 이 체인코드를 사용하는 채널에 있는 모든 피어에서 체인코드를 업데이트해야 합니다. 체인코드를 업데이트하려면 다음 단계를 완료하십시오.

1. 이전 체인코드와 이름이 동일하지만 버전이 다른 체인코드를 설치하십시오. [체인코드 설치](/docs/services/blockchain/howto/install_instantiate_chaincode.html#install-instantiate-chaincode-install-cc)와 동일한 단계를 따를 수 있습니다. 원래 체인코드와 동일한 채널을 선택했는지 확인하십시오.

  ![체인코드 업데이트](../images/upgrade_chaincode.png "체인코드 업데이트")

2. 테이블에서 새 체인코드를 찾은 후 **조치** 헤더 아래의 **업데이트** 단추를 클릭하십시오. 이 조치는 체인코드를 다시 인스턴스화하고 체인코드 컨테이너를 새 체인코드 컨테이너로 대체합니다. **업데이트** 단추를 클릭하면 체인코드 보증 정책을 업데이트할 수 있으며,
조직이 최근 채널에 추가된 경우 수행해야 하는 작업입니다. 업데이트 기능의 일부로 새 인수를 입력할 필요는 없습니다. 이 업그레이드 조치는 채널에서 발생하며 하나의 조직에서만 수행되어야 합니다.

  ![업데이트 단추](../images/upgrade_button.png "업데이트 단추")
