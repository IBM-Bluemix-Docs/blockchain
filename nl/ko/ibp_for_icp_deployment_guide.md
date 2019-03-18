---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-05"

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

# {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private으로 시작하기
{: #get-started-icp}

{{site.data.keyword.blockchainfull}} Platform for {{site.data.keyword.cloud_notm}} Private을
사용하면 사용자가 {{site.data.keyword.cloud_notm}} Private 등의 온프레미스 환경에서 Kubernetes Helm 차트를
사용하여 x86, LinuxONE 및 IBM Z에 인증 기관(CA), 순서 지정자 및 피어를 배치하고
다중 클라우드 환경에서 호스팅되는 컴포넌트에 연결할 수 있습니다. {{site.data.keyword.cloud_notm}} Private는
온프레미스 컨테이너화 애플리케이션을 개발하고 관리하는 데 사용하는 애플리케이션 플랫폼입니다. 이는
컨테이너 오케스트레이터 Kubernetes, 개인용 이미지 레지스트리, 관리 콘솔 및 모니터링 프레임워크가 포함된 컨테이너를 관리하기 위한 통합 환경입니다.
{:shortdesc}

[Hyperledger Fabric](https://hyperledger-fabric.readthedocs.io/en/release-1.2/)을 기반으로 하는 블록체인 네트워크는 거의 무한한 배열의 구성으로 배치되어 많은 유스 케이스를 지원할 수 있습니다. 이러한 유연성에도 불구하고 네트워크 컴포넌트를 설정하고 배치하려면 올바른 **순서**와 관련한 여러 가지 우수 사례가 존재합니다.

이 배치 안내서는 배치 시 고려해야 할 우수 사례 및 고려사항 외에도 {{site.data.keyword.cloud_notm}} Private에서 작동하는 {{site.data.keyword.blockchainfull}} 플랫폼 네트워크를 설정하기 위한 올바른 순서를 표시합니다. 그러나 작동 중인 CA, 순서 지정자 또는 피어만 설정하려는 경우 기본 규칙이 계속 적용됩니다. 단일 순서 지정자 노드만 배치하는 SOLO 순서 지정 서비스는 프로덕션 환경용이 아님을 유의하십시오. SOLO를 실행하는 네트워크 또는 채널도 "프로덕션" 환경으로 간주될 수 없습니다. 그러나 특히 가용성이 높은 경우 프로덕션 환경에서 피어 및 CA를 배치할 수 있습니다.

{{site.data.keyword.cloud_notm}} Private에 {{site.data.keyword.blockchainfull_notm}} Platform을
배치하는 프로세스는 어렵고 Fabric에 대한 높은 전문 지식이 필요합니다. Fabric, {{site.data.keyword.blockchainfull_notm}} Platform 또는
{{site.data.keyword.cloud_notm}} Private을 처음 사용하고 개발 환경 또는 PoC(proof of concept)를 설정하는 것이 목표라면 대신
[스타터 플랜](/docs/services/blockchain/starter_plan.html#starter-plan-about)을 사용하는 것을 고려하십시오. 또한 잠재적인 모든 배치 구성이 지원되는 것은 아닙니다. 어렵기 때문에 Fabric 전문가가 관리 업무를 다른 당사자에게 넘기기 전에 배치 프로세스와 컴포넌트를 서로 연결하는 과정을 거치는 것으로 가정합니다. 해당 전문가가 이 안내서 및 일반적으로 제공하는 Helm 차트 컴포넌트에 대한 문서의 대상 독자입니다.
{:important}

## 1단계: 네트워크 구성 결정

블록체인 네트워크의 구조는 유스 케이스에 의해 결정되어야 합니다. 이러한 근본적인 비즈니스 의사결정은 다양한 상황에 따라 다르지만 몇 가지를 고려하도록 합니다.

* **개발 환경** 설정

  [스타터 플랜](/docs/services/blockchain/starter_plan.html#starter-plan-about)에서 빌드하지만 개발 환경에서 자체 컴포넌트를 관리하려는 경우 순서 지정자와 피어(각 조직마다 하나의 CA 사용)로 구성된 기본 구성이 필요합니다. 각 조직에 대해 [fabcar 네트워크](https://hyperledger-fabric.readthedocs.io/en/release-1.2/understand_fabcar_network.html) 구성과 유사한 단일 순서 지정자 및 단일 피어만 사용하기로 결정할 수 있습니다. 마찬가지로 각 컴포넌트에 대해 별도의 사용자를 작성하는 대신 이러한 모든 컴포넌트에 대해 단일 관리자만 필요할 수도 있습니다.

* 새 네트워크 또는 기존 네트워크에 **프로덕션 컴포넌트** 배치

  프로덕션 컴포넌트와 프로덕션 네트워크에는 개발 환경 또는 PoC(proof of concept)와 다른 요구사항이 있습니다. 우선, 고가용성이 우선순위가 됩니다. SOLO 순서 지정 서비스(따라서 단일 실패 지점)만 포함하는 단일 순서 지정 서비스는 정의상 프로덕션용이 아닙니다.

**참고:** 이 배치 안내서는 모든 반복 및 잠재적인 네트워크 구성을 거치지는 않지만 고려해야 할 일반 가이드라인 및 규칙을 제공합니다.

## 2단계: {{site.data.keyword.cloud_notm}} Private에서 Kubernetes 클러스터 설정

네트워크 구조를 결정한 후 유스 케이스에 맞게 {{site.data.keyword.cloud_notm}} Private에 Kubernetes 클러스터를 설정하십시오. 자세한 정보는
[{{site.data.keyword.cloud_notm}} Private 설정](/docs/services/blockchain/ICP_setup.html#icp-setup)을 참조하십시오.

## 3단계: CA 설정

Fabric 기반 블록체인 네트워크에서 배치해야 할 첫 번째 컴포넌트는 CA입니다. 컴포넌트의 구성에 컴포넌트를 배치하기 전에 해당 컴포넌트를 작동할 권한이 부여된 하나 이상의 사용자 ID를 포함해야 하기 때문입니다.

종종 이는 개념적으로 이해하기 어려울 수 있습니다. 예를 들면, 랩탑과 같은 전자 디바이스는 새로운 경우 누구나 액세스할 수 있습니다. 디바이스를 켜는 첫 번째 사용자는 "소유자"로 간주되므로 이후의 모든 사용자가 알아야 할 비밀번호를 등록하고 설정할 수 있습니다. 그러나 이 방식은 Fabric 기반 블록체인 네트워크에서 컴포넌트가 설정되는 방법이 아닙니다. 피어와 순서 지정자가 처음 배치될 때 피어와 순서 지정자에 빌드된 관리 정보가 있어야 합니다.

**조직당 하나의 CA를 배치하도록 권장됩니다.** 예를 들어, 하나의 조직과 연관된 세 개의 피어와 다른 조직과 연관된 순서 지정자를 배치하려는 경우 두 개의 CA를 배치해야 합니다. 하나의 CA는 피어 조직용이고 다른 하나는 순서 지정자 조직용입니다.

CA의 무한 회귀(모든 CA가 다른 CA와 계속 링크되어야 하는 경우)를 방지하기 위해 CA에는 기본 사용자 이름과 비밀번호 쌍이 연관되어 있습니다. CA가 배치될 때 이 사용자 이름 및 비밀번호를 지정합니다. 이 CA는 컴포넌트의 신뢰 루트인 "루트 CA"입니다. 프로덕션 네트워크에서 이 루트 CA에서 인증서를 가져오는 하나 이상의 다른 CA를 배치하고 "중간 CA"인 해당 CA를 사용하여 사용자와 컴포넌트에 인증서를 발행하는 것이 좋습니다. 그러나 이 릴리스에서는 중간 CA의 사용은 지원되지 않습니다.

모든 조직에는 등록에 필요한 CA와 TLS CA가 있어야 합니다.  {{site.data.keyword.cloud_notm}} Private에 CA를 배치할 때 TLS CA도 기본적으로 동일한 컨테이너에 배치됩니다. 이 TLS CA에서 TLS 인증서를 생성하고 관리합니다. 스타터 또는 엔터프라이즈 플랜 네트워크에 있는 CA에는 TLS CA가 포함되어 있지 않지만 등록에 사용되는 CA는 포함되어 있습니다. 따라서 스타터 또는 엔터프라이즈 플랜 네트워크에 피어를 연결하려면 피어를 배치하기 전에 해당 피어의 TLS CA로 사용할 [{{site.data.keyword.cloud_notm}} Private에 CA도 배치](/docs/services/blockchain/howto/CA_deploy_icp.html#ca-deploy)해야 합니다. [{{site.data.keyword.blockchainfull_notm}} Platform에 {{site.data.keyword.cloud_notm}} Private 피어를 연결하기 위한 전제조건](/docs/services/blockchain/howto/peer_deploy_ibp.html#ibp-peer-deploy-prerequisites)도 참조하십시오. TLS CA는 인증서 발행에만 사용되며 해당 활동이 완료되면 종료될 수 있다는 점에 유의하십시오.

TLS에 대한 자세한 정보는 Hyperledger Fabric 문서에서 [TLS(Transport Layer Security)로 통신 보안 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://hyperledger-fabric.readthedocs.io/en/release-1.3/enable_tls.html "TLS(Transport Layer Security)로 통신 보안")의 내용을 참조하십시오.

### 순서 지정자 및 피어의 MSP 준비

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private 프로세스는 매우 정교하므로 초기 설정 동안 모든 네트워크 컴포넌트 노드에 대한 관리자로서 단일 관리자 ID를 사용하는 것이 좋습니다. 이렇게 하면 한 사용자가 다양한 컴포넌트 간에 구성과 연결을 설정하여 올바르게 작동하는지 확인하여 배치 및 연결 오류를 줄일 수 있습니다. 그러나 각 컴포넌트에 서로 다른 인증서가 있어야 하는 것은 매우 중요합니다. 때로는 여기서 구별하기가 쉽지 않을 수 있습니다. 트랜잭션 제안에 서명하는 엔티티는 피어의 관리자가 아니라 **피어 자체**입니다. 따라서 피어는 등록되어 있어야 하며 피어에는 수행하는 모든 작업에 접속하는 인증서와 특정 종류의 서명을 생성하는 데 사용할 수 있는 개인 키가 있어야 합니다. Fabric 기반 블록체인 네트워크의 ID와 권한에 대한 자세한 정보는 Fabric 문서의 [ID ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://hyperledger-fabric.readthedocs.io/en/release-1.3/identity/identity.html "ID") 및 [멤버십 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://hyperledger-fabric.readthedocs.io/en/release-1.3/membership/membership.html "멤버십")을 참조하십시오.

[CA 운영에 관한 문서](/docs/services/blockchain/howto/CA_operate.html#ca-operate-fabric-ca-client)의 지시사항을 수행하여 설치되어야 하는 Fabric CA client는 ID를 등록하는 데 사용됩니다. 이 ID는 배치할 네트워크 컴포넌트의 관리자로 구성을 변경하고 컴포넌트를 함께 연결할 수 있게 합니다. 이후 이러한 컴포넌트의 관리를 다른 사용자에게 이전하려면 해당 컴포넌트에 대한 새 관리자를 등록한 다음 필요한 경우 관리자로서 사용자를 제거할 수 있습니다.

순서 지정자 또는 피어가 배치될 때 순서 지정자 또는 피어와 연관된 `init` 컨테이너는 Kubernetes 시크릿 오브젝트를 사용하여 컴포넌트에 대한 MSP를 작성합니다. 시크릿 오브젝트를 작성하는 방법을 알아보려면 [CA 운영](/docs/services/blockchain/howto/CA_operate.html#ca-operate)을 참조하십시오. 위에서 설명한 대로 CA를 설정하고 각 조직에 대해 이 플로우를 반복해야 함을 기억하십시오.

## 4단계: 순서 지정자 및 피어 배치

Kubernetes 시크릿이 작성되면 컴포넌트를 배치할 준비가 되었습니다. 채널을 설정하려는 경우 피어 전에 순서 지정자를 배치하도록 권장됩니다. 모든 컴포넌트에 다른 조직 이름을 사용해야 합니다.

- **[순서 지정자 배치](/docs/services/blockchain/howto/orderer_deploy_icp.html#icp-orderer-deploy)**. 현재 SOLO 순서 지정 서비스만 지원됩니다. 계산과 관련된 배치 프로세스에는 옵션이 있습니다.

- **[{{site.data.keyword.cloud_notm}} Private 순서 지정자에 연결될 피어 배치](/docs/services/blockchain/howto/peer_deploy_icp.html#icp-peer-deploy)**. Helm 차트에서 지정할 수 있는 데이터베이스 유형을 포함하여 피어를 배치하는 데 필요한 여러 가지 옵션이 있습니다. 피어의 조직 MSP ID가 순서 지정자의 조직 MSP ID와 다른지 확인하십시오.

- **[{{site.data.keyword.blockchainfull_notm}} Platform 네트워크에 연결될 피어 배치](/docs/services/blockchain/howto/peer_deploy_ibp.html#ibp-peer-deploy)**. 연결 프로파일과 네트워크 모니터 UI를 사용하므로 피어를 배치하는 프로세스와 {{site.data.keyword.cloud_notm}}의 [스타터 플랜](/docs/services/blockchain/starter_plan.html#starter-plan-about) 또는 [엔터프라이즈 플랜](/docs/services/blockchain/enterprise_plan.html#enterprise_plan-about) 네트워크에 연결하는 프로세스는 다릅니다. 피어가 속한 조직은 이미 네트워크의 채널에 가입되어 있어야 함에 유의하십시오. 다시 한 번 피어의 조직 MSP ID가 순서 지정자의 조직 MSP ID와 다른지 확인하십시오.

## 다음 단계

모든 노드를 배치한 후에 노드를 작동시키고 트랜잭션을 제출할 수 있습니다. 추가 정보는 다음 링크를 참조하십시오.

- [{{site.data.keyword.cloud_notm}} Private에서 인증 기관 작동](/docs/services/blockchain/howto/CA_operate.html#ca-operate)
- [{{site.data.keyword.cloud_notm}} Private에서 순서 지정자 작동](/docs/services/blockchain/howto/orderer_operate.html#icp-orderer-operate)
- [다중 클라우드 네트워크에서 {{site.data.keyword.cloud_notm}} Private 작동](/docs/services/blockchain/howto/peer_operate_icp.html#icp-peer-operate)
- [스타터 플랜 또는 엔터프라이즈 플랜으로 {{site.data.keyword.cloud_notm}} Private에서 피어 작동](/docs/services/blockchain/howto/peer_operate_icp.html#icp-peer-operate)

## 네트워크 확장

목표가 개발 환경 또는 PoC(proof of concept) 설정인 경우 순서 지정자의 배치 중에 작성되는 순서 지정자 시스템 채널에 피어 조직을 추가해야 합니다. 이는 모든 컴포넌트를 활용하는 다단계 프로세스로 관련 운영 주제에 문서화되어 있습니다.

1. 조직을 추가하기 전에 작성하고 해당 MSP ID를 설정해야 합니다. [CA 운영](/docs/services/blockchain/howto/CA_operate.html#ca-operate-deploy-orderer-peer)을 참조하십시오.

2. 조직이 작성되면 순서 지정자 시스템 채널에 추가될 수 있습니다. 자세한 정보는 [순서 지정자 운영](/docs/services/blockchain/howto/orderer_operate.html#icp-orderer-operate-add-organizations-to-consortium)을 참조하십시오.

3. 조직이 순서 지정자 시스템 채널에 나열되면 "컨소시엄"의 멤버이며 트랜잭션이 발생하는 채널의 유형인 애플리케이션 채널을 작성할 수 있습니다. 채널 작성 방법에 대한 자세한 정보는 [채널 작성](/docs/services/blockchain/howto/peer_operate_icp.html#icp-peer-operate-create-channel)을 참조하십시오.
