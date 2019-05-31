---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-05"

keywords: IBM Blockchain offerings, Linux Foundation, Hyperledger Fabric, open source, community contribution

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:note: .note}
{:important: .important}
{:tip: .tip}

# 면책사항
{: #disclaimer}

**주의:** {{site.data.keyword.blockchainfull}} 플랜을 사용하기 전에 다음 정보를 검토해야 합니다.

## IBM 지원 설명
{: #disclaimer-support-statement}

{{site.data.keyword.IBM}}은 오랜 시간 혁신의 선두 자리를 지켜왔으며 {{site.data.keyword.cloud_notm}}의 {{site.data.keyword.blockchainfull_notm}} Platform 오퍼링을 통해 여전히 그 역할을 계속하고 있습니다. 블록체인은 금융 산업, 로컬 및 글로벌 공급 체인과 많은 비즈니스 영역에서 업무 조직에 관한 지원을 중단하도록 보호되는 기술입니다. 다양한 조기 도입 프로그램을 통해 {{site.data.keyword.IBM_notm}} 고객 및 비즈니스 파트너는 산업용 솔루션으로서 블록체인을 활발하게 이용해 오고 있습니다. {{site.data.keyword.blockchainfull_notm}} Platform on {{site.data.keyword.cloud_notm}}가 그러한 프로그램 중 하나입니다. **다른 새 기술의 경우와 같이 {{site.data.keyword.blockchainfull_notm}} Platform on {{site.data.keyword.cloud_notm}} 사용자는 신속하고 근본적인 변화의 가능성에 대해 인지하고 있어야 합니다.**
{:shortdesc}

{{site.data.keyword.blockchainfull_notm}}을 뒷받침하는 아키텍처는 Linux Foundation의 Hyperledger Fabric 프로젝트입니다. 각 오픈 소스 커뮤니티 컨트리뷰션은 Hyperledger Fabric을 개선하지만 적용에 어려움이 있을 수 있습니다. **{{site.data.keyword.IBM_notm}}은 Hyperledger Fabric 블록체인 네트워크에서 금융 자산을 직접 정의하거나 교환하는 것에 대해 경고하고 있습니다**.

{{site.data.keyword.IBM_notm}}은 Composer CLI, JavaScript API, REST 서버 및 웹 플레이그라운드를 포함하여 프로덕션에서 Hyperledger Composer를 사용하는 네트워크를 지원하지 않습니다.
{:note}

## 오픈 소스 명령문
{: #disclaimer-open-source-statement}

{{site.data.keyword.cloud_notm}}의 {{site.data.keyword.blockchainfull_notm}} 오퍼링 플랜은 Linux Foundation의 Hyperledger Fabric 스택을 기반으로 빌드되었습니다. {{site.data.keyword.IBM_notm}}을 포함한 Hyperledger 프로젝트 멤버는 Hyperledger 보호 아래 다양한 하위 프로젝트에 계속 기여합니다.  모든 컨트리뷰션은 커뮤니티에서 검토, 조사하고 테스트합니다.

## 체인코드 지원 설명
{: #disclaimer-chaincode-support-statement}

다음 코딩 방식은 {{site.data.keyword.blockchainfull_notm}} 네트워크에서 지원되지 않습니다.

1. 반복에 연관 배열 사용(Go에서 순서가 무작위로 지정됨)
2. KVS 테이블에서 항목 목록 읽기(순서가 보장되지 않음)
3. 스레드에 대해 안전하지 않은 체인코드 작성(조회와 호출을 동시에 호출할 수 있음).
4. 체인코드에서 원장 상태 변수를 글로벌 메모리 또는 캐시 스토리지로 대체
5. 체인코드에서 직접 데이터베이스와 같은 외부 서비스에 액세스
6. 비결정성을 야기시킬 수 있는 글로벌 변수 또는 라이브러리 사용(예: "random" 또는 "time" 사용)

또한, 데이터 일관성 및 무결성에 위험이 발생할 수 있는 비결정적 체인코드 작성은 권장되지 않습니다. Hyperledger Fabric 아키텍처는 일련의 보증 및 유효성 검증 검사를 통해 비결정적 체인코드에 대응하도록 설계되었습니다. 하지만 여전히 비정적 글로벌 변수(예: 시간)에 의존하지 않는 결정 함수를 코딩하도록 권장됩니다.
