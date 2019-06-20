---

copyright:
  years: 2019
lastupdated: "2019-05-31"

keywords: troubleshooting, debug, why, what does this mean, how can I, when I

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# 문제점 해결
{: #ibp-v2-troubleshooting}

콘솔을 사용하여 노드, 채널 또는 스마트 계약을 관리할 때 일반 문제가 발생할 수 있습니다. 대부분의 경우 몇 개의 간단한 단계를 수행하면 이러한 문제점으로부터 복구할 수 있습니다.
{:shortdesc}

- [내 노드 위에 마우스를 올려 놓으면 상태는 `Status unavailable`이 됩니다. 이는 무엇을 의미합니까?](#ibp-v2-troubleshooting-status-unavailable)
- [내 노드 위에 마우스를 올려 놓으면 상태는 `Status undetectable`이 됩니다. 이는 무엇을 의미합니까?](#ibp-v2-troubleshooting-status-undetectable)
- [피어 또는 순서 지정자를 작성한 후 내 노드 작동이 실패하는 이유는 무엇입니까? ](#ibp-console-build-network-troubleshoot-entry1)
- [피어가 시작하지 못하는 이유는 무엇입니까?](#ibp-console-build-network-troubleshoot-entry2)
- [스마트 계약 설치, 인스턴스화 또는 업그레이드에 실패하는 이유는 무엇입니까? ](#ibp-console-smart-contracts-troubleshoot-entry1)
- [스마트 계약 컨테이너 로그를 보려면 어떻게 해야 합니까? ](#ibp-console-smart-contracts-troubleshoot-entry2)
- [채널, 스마트 계약 및 ID가 콘솔에서 사라졌습니다. 어떻게 하면 되돌릴 수 있습니까?](/docs/services/blockchain/howto/ibp-v2-troubleshooting.html#ibp-v2-troubleshooting-browser-storage)
- [조직 MSP 정의를 새로 작성할 때 `제공한 등록 ID와 시크릿으로 인증할 수 없음` 오류가 표시되는 이유는 무엇입니까?](#ibp-v2-troubleshooting-create-msp)
- [내 채널에 조직을 추가하려고 할 때 `채널 업데이트 중 오류 발생` 오류가 발생하는 이유는 무엇입니까?](#ibp-v2-troubleshooting-update-channel)
- [내 Kubernetes 클러스터가 만료되었습니다. 이는 무엇을 의미합니까?](#ibp-v2-troubleshooting-cluster-expired)
- [VS Code에서 제출하는 트랜잭션이 실패하는 이유는 무엇입니까?](#ibp-v2-troubleshooting-anchor-peer)
- [내 콘솔에 로그인하면 401 권한 없음 오류가 표시됩니다.](#ibp-v2-troubleshooting-console-401)

## 내 노드 위에 마우스를 올려 놓으면 상태는 `Status unavailable`이 됩니다. 이는 무엇을 의미합니까?
{: #ibp-v2-troubleshooting-status-unavailable}
{: troubleshoot}

CA, 피어 또는 순서 지정자 노드에 대한 타일의 노드 상태가 회색이며, 이는 노드의 상태가 사용 불가능함을 의미합니다. 이상적으로 노드 위에 마우스를 올려 놓으면 노드 상태는 `Running`이어야 합니다.
{: tsSymptoms}

노드가 새로 작성되고 배치 프로세스가 완료되지 않은 경우 이 문제가 발생할 수 있습니다. 노드가 CA이면 노드가 실행 중이지 않을 수 있습니다.
이 노드가 피어 또는 순서 지정자인 경우 이 상태는 피어 또는 순서 지정자 노드에 대해 실행되는 상태 검사기가 노드에 연결할 수 없는 경우에 발생합니다.  노드가 특정 시간 내에 응답하지 않거나, 노드가 작동 중지될 수 있거나, 네트워크 연결이 끊어진 이유로 상태에 대한 요청이 제한시간 초과 오류로 실패할 수 있습니다.
{: tsCauses}

새 노드인 경우 배치가 완료될 때까지 몇 분 더 기다리십시오. 새 노드가 아닌 경우
오류를 판별하려면 오류에 대한 [연관된 노드 로그를 조사](/docs/services/blockchain/howto/ibp-console-manage.html#ibp-console-manage-console-node-logs)하십시오.
{: tsResolve}

## 내 노드 위에 마우스를 올려 놓으면 상태는 `Status undetectable`이 됩니다. 이는 무엇을 의미합니까?
{: #ibp-v2-troubleshooting-status-undetectable}
{: troubleshoot}

피어 또는 순서 지정자 노드에 대한 타일의 노드 상태가 노란색이며, 이는 노드의 상태가 발견될 수 없음을 의미합니다. 이상적으로 노드 위에 마우스를 올려 놓으면 노드 상태는 `Running`이어야 합니다.
{: tsSymptoms}

이 상태는 콘솔로 *가져온* 피어 및 순서 지정자 노드에서만 발생하고 상태 검사기는 노드에 대해 실행할 수 없습니다. 노드를 가져올 때 `operations_url`이 지정되지 않았으므로 이 상태가 발생합니다. 노드 상태 검사기가 실행되려면 오퍼레이션 URL이 필요합니다. 노드 자체는 `Running`일 수 있으나 오퍼레이션 URL이 지정되지 않았으므로 상태를 판별할 수 없습니다.
{: tsCauses}

다음 단계를 수행하여 이 문제점을 해결할 수 있습니다.
 1. 노드 타일을 클릭하여 여십시오.
 2. **설정** 아이콘을 클릭하십시오.
 3. **ID 연관**을 클릭하고 이 노드와 연관되는 ID를 확인하고 기록해 두십시오. **취소**를 클릭하여 이 패널을 닫으십시오.
 4. **내보내기**를 클릭하여 노드에 대한 `JSON` 파일을 생성하십시오.
 5. 생성된 `JSON` 파일을 편집하고 노드에 대한 `operations_url`을 입력하십시오. `operations_url` 값은 구성 방식 및 다양한 네트워크 설정에 따라 달라집니다. 이 값은 노드를 배치한 네트워크 관리자가 제공해야 합니다.
 6. **삭제**를 클릭하십시오. 이 단계는 콘솔에서 가져온 노드를 제거하지만 실제 노드는 삭제하지 않습니다.
 7. **노드** 탭에서 **피어 추가** 또는 **순서 지정자 추가**를 클릭한 후 **기존 피어 가져오기** 또는 **기존 순서 지정자 가져오기**를 클릭하십시오.
 8. **JSON 업로드**를 클릭한 후 방금 편집한 JSON 파일을 찾아보십시오. **다음**을 클릭하십시오.
 9. 3단계에서 기록해 놓은 동일한 ID를 연관시키십시오.
 10. **피어 추가** 또는 **순서 지정자 추가**를 클릭하십시오.

상태 검사기가 이제 노드에 대해 실행되며 노드의 상태를 보고할 수 있습니다.
{: tsResolve}

## 피어 또는 순서 지정자를 작성한 후 내 노드 작동이 실패하는 이유는 무엇입니까?
{: #ibp-console-build-network-troubleshoot-entry1}
{: troubleshoot}

기존 노드를 관리할 때 오류가 발생할 수 있습니다. 이런 경우에는 대개 노드 로그를 참조하는 것이 유용합니다.  

예를 들어 노드를 작동하려고 할 때 조치가 실패할 수 있습니다.
{: tsSymptoms}

피어 또는 순서 지정자를 새로 작성한 후에는 클러스터 스토리지 구성에 따라 노드 작동 준비가 완료될 때까지 몇 분 정도 소요될 수 있습니다.
{: tsCauses}

Kubernetes 대시보드를 확인하고 피어 또는 노드 상태가 `Running`인지 확인하십시오. 그런 다음 조치를 다시 시도하십시오. 노드가 작동된 후에도 여전히 문제가 발생하는 경우에는 [노드 로그](/docs/services/blockchain/howto/ibp-console-manage.html#ibp-console-manage-console-node-logs)에서 오류가 있는지 확인하십시오.  
{: tsResolve}

## 피어가 시작하지 못하는 이유는 무엇입니까?
{: #ibp-console-build-network-troubleshoot-entry2}
{: troubleshoot}

이 오류는 다양한 상황에서 발생할 수 있습니다.

피어 로그에는 `2019-02-06 19:43:24.159 UTC [main] InitCmd -> ERRO 001 Cannot run peer because cannot init crypto, folder “/certs/msp” does not exist`가 포함되어 있습니다.
{: tsSymptoms}

- 이 오류는 다음 상황에서 발생할 수 있습니다.
  - 피어 또는 순서 지정자의 조직 MSP 정의를 작성할 때 `client`가 아닌 `peer` 유형의 ID에 해당하는 등록 ID 및 시크릿을 지정했습니다. `client` 유형이어야 합니다.
  - 피어 또는 순서 지정자의 조직 MSP 정의를 작성할 때 해당 조직 관리자 ID의 등록 ID 또는 시크릿과 일치하지 않는 등록 ID 및 시크릿을 지정했습니다. 
  - 피어 또는 순서 지정자를 작성할 때 'peer' 유형이 아닌 ID의 등록 ID 및 시크릿을 지정했습니다. 

- 피어 또는 순서 지정자 CA 노드를 열고 **등록된 사용자** 테이블에 나열된 등록된 ID를 확인하십시오.
- 피어 또는 순서 지정자를 삭제하고 올바른 등록 ID 및 시크릿을 신중히 지정하여 다시 작성하십시오. 
- 피어 또는 순서 지정자를 작성하기 전에 'client' 유형의 조직 관리자 ID를 작성해야 합니다. 조직 MSP 정의를 작성할 때 등록 ID와 동일한 ID를 지정해야 합니다. [피어 ID 등록](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network-use-CA-org1) 및 [순서 지정자 ID 등록](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network-use-CA-orderer)에 대해서는 이러한 지침을 참조하십시오.
{: tsResolve}

## 스마트 계약 설치, 인스턴스화 또는 업그레이드에 실패하는 이유는 무엇입니까?
{: #ibp-console-smart-contracts-troubleshoot-entry1}
{: troubleshoot}

스마트 계약을 설치, 인스턴스화 또는 업그레이드할 때 오류가 발생할 수 있습니다.  예를 들어 스마트 계약을 피어에 설치하려고 할 때 `피어에 스마트 계약을 설치할 때 오류가 발생했습니다.`라는 오류가 발생하면서 실패합니다.
{: tsSymptoms}

이 버전의 스마트 계약이 이미 피어에 있거나 피어의 리소스가 부족한 경우에 이 오류를 수신할 수 있습니다.
{: tsCauses}

- Kubernetes 대시보드를 열고 피어 상태가 `Running`인지 확인하십시오.  
- 피어 노드를 열고 스마트 계약 버전이 이미 피어에 존재하지 않는지 확인하고 올바른 버전으로 다시 시도하십시오.
- 노드가 작동된 후에도 여전히 문제가 발생하는 경우에는 [노드 로그](/docs/services/blockchain/howto/ibp-console-manage.html#ibp-console-manage-console-node-logs)에서 오류가 있는지 확인하십시오.  
{: tsResolve}

## 스마트 계약 컨테이너 로그를 보려면 어떻게 해야 합니까?
{: #ibp-console-smart-contracts-troubleshoot-entry2}
{: troubleshoot}

스마트 계약 문제를 디버깅하기 위해 스마트 계약 또는 체인코드, 컨테이너 로그를 확인해야 할 수도 있습니다.
{: tsSymptoms}

이 지침에 따라 [컨테이너 로그를 확인](/docs/services/blockchain/howto/ibp-console-manage.html#ibp-console-manage-console-container-logs)하십시오.
{: tsResolve}

## 채널, 스마트 계약 및 ID가 콘솔에서 사라졌습니다. 어떻게 하면 되돌릴 수 있습니까?
{: #ibp-v2-troubleshooting-browser-storage}
{: troubleshoot}

콘솔 지갑 ID는 블록체인 컴포넌트를 관리할 수 있도록 하는 서명 인증서 및 개인 키로 구성되지만, 브라우저 로컬 스토리지에만 저장됩니다. 이러한 ID를 보호하고 관리할 책임은 사용자에게 있습니다. 해당 ID를 작성한 후 파일 시스템으로 내보내는 것이 좋습니다. 노드를 새로 작성할 때 콘솔 지갑의 ID를 노드와 연관시키십시오. 이 관리자 ID를 사용하여 노드를 관리할 수 있습니다. 브라우저를 전환하거나 다른 시스템의 브라우저로 변경할 경우 해당 ID는 더 이상 지갑에 없습니다. 따라서 컴포넌트를 관리할 수 없습니다.
{: tsSymptoms}

{{site.data.keyword.blockchainfull_notm}} Platform의 새로운 기능 중 하나는 이제 인증서를 보안 설정하고 관리하는 책임이 사용자에게 있다는 점입니다. 따라서 사용자가 컴포넌트를 관리할 수 있도록 인증서가 브라우저 로컬 스토리지에만 저장됩니다. 개인용 브라우저 창을 사용한 후 다른 브라우저 또는 개인용이 아닌 브라우저 창으로 전환하는 경우 작성한 ID가 새 브라우저 세션의 콘솔 지갑에서 사라집니다. 그러므로 ID를 개인용 브라우저 세션의 콘솔 지갑에서 파일 시스템으로 내보내야 합니다. 그런 다음 ID가 필요한 경우 ID를 개인용이 아닌 브라우저 세션에 가져올 수 있습니다. 그렇지 않으면 ID를 복구할 수 있는 방법이 없습니다.
{: tsCauses}

- 새 조직 MSP 정의를 새로 작성할 때 언제든지 조직을 관리할 수 있는 ID에 대한 키를 생성할 수 있습니다. 따라서 해당 프로세스 중에는 **생성** 및 **내보내기** 단추를 차례로 클릭하여 생성된 ID를 콘솔 지갑에 저장한 후 파일 시스템에 JSON 파일로 저장해야 합니다.
- 브라우저에서 이 문제점을 해결하려면 해당 ID를 가져와서 해당 노드와 연관시켜야 합니다.
  - 문제점이 발생한 브라우저에서 **지갑** 탭을 클릭한 후 **ID 추가**를 클릭하여 JSON 파일을 지갑으로 가져오십시오.
  - **JSON 업로드**를 클릭한 후 **파일 추가** 단추를 사용하여 내보낸 JSON 파일을 찾아보십시오.
  - **제출**을 클릭하십시오.
  - 이제 이 ID와 원래 연관된 피어 또는 순서 지정자 노드를 열고 **설정** 아이콘을 클릭하십시오.
  - **ID 연관** 단추를 클릭하십시오.
  - 드롭 다운 목록에서 방금 콘솔 지갑으로 가져온 ID를 선택하십시오.
  - **연관**을 클릭하십시오.
- 원래 브라우저의 지갑에 있었던 각 ID에 대해 이 프로세스를 반복하십시오.
{: tsResolve}

## 조직 MSP 정의를 새로 작성할 때 `제공한 등록 ID와 시크릿으로 인증할 수 없음` 오류가 표시되는 이유는 무엇입니까? 
{: #ibp-v2-troubleshooting-create-msp}
{: troubleshoot}

조직 탭에서 조직 MSP 정의를 새로 작성하려고 하면 `제공한 등록 ID와 시크릿으로 인증할 수 없음` 오류가 발생합니다.
{: tsSymptoms}

이 오류는 등록 시크릿에 대해 지정한 값이 패널의 `조직 관리자 인증서 생성` 섹션에서 선택한 등록 ID에 올바르지 않은 경우에 발생합니다.
{: tsCauses}

등록 ID 드롭 다운 입력에서 올바른 조직 관리자 등록 ID를 선택했는지 확인한 후 올바른 등록 시크릿 값을 입력하십시오.
{: tsResolve}

## 내 채널에 조직을 추가하려고 할 때 `채널 업데이트 중 오류 발생` 오류가 발생하는 이유는 무엇입니까?
{: #ibp-v2-troubleshooting-update-channel}
{: troubleshoot}

채널에 다른 조직을 추가하려고 하면 `채널 업데이트 중 오류 발생` 메시지와 함께 업데이트가 실패합니다.
{: tsSymptoms}

이 오류는 **채널 업데이트** 패널에서 선택한 **채널 업데이트 MSP ID**가 채널 관리자가 아닌 경우에 발생합니다.
{: tsCauses}

**채널 업데이트** 패널에서 아래로 스크롤하여 **채널 업데이트 MSP ID**로 이동한 후 채널 작성 시 지정한 MSP ID를 선택하거나 채널 관리자의 MSP ID를 지정하십시오.
{: tsResolve}

## 내 Kubernetes 클러스터가 만료되었습니다. 이는 무엇을 의미합니까?
{: #ibp-v2-troubleshooting-cluster-expired}
{: troubleshoot}

내 {{site.data.keyword.IBM_notm}} Kubernetes Service 클러스터가 만료될 예정이며 해당 상태가 `Expired`라는 이메일을 수신했습니다. 또는 30일 후에는 콘솔에 액세스할 수 없습니다.
{: tsSymptoms}

무료 Kubernetes 클러스터는 30일 동안만 유효합니다.
{: tsCauses}

무료 클러스터에서 유료 클러스터로 마이그레이션할 수 없습니다. 30일 후에는 콘솔에 액세스할 수 없고 모든 노드 및 인증서가 삭제됩니다. 발생한 사항 및 수행할 수 있는 조치에 대한 정보는 [Kubernetes 클러스터 만기](/docs/services/blockchain/howto/ibp-console-manage.html#ibp-console-manage-console-cluster-expiration)에 대한 주제를 참조하십시오.
{: tsResolve}

## VS Code에서 제출하는 트랜잭션이 실패하는 이유는 무엇입니까?
{: #ibp-v2-troubleshooting-anchor-peer}
{: troubleshoot}

VS Code에서 제출된 트랜잭션이 다음과 유사한 오류와 함께 실패합니다.
```
Error submitting transaction: No endorsement plan available for {"chaincodes":[{"name":"hello-world"}]}
```
{: tsSymptoms}

이 오류는 Fabric 서비스 발견 기능을 사용 중이지만 채널에 앵커 피어를 구성하지 않은 경우에 발생합니다.
{: tsCauses}

앵커 피어를 구성하려면 스마트 계약 배치 튜토리얼에서 [개인용 데이터 주제](/docs/services/blockchain/howto/ibp-console-smart-contracts.html#ibp-console-smart-contracts-private-data)의 3단계를 따르십시오.

## 내 콘솔에 로그인하면 401 권한 없음 오류가 표시됩니다. 
{: #ibp-v2-troubleshooting-console-401}
{: troubleshoot}

내 콘솔에 로그인하려고 할 때 브라우저에서 콘솔에 액세스할 수 없습니다. 브라우저 로그를 확인하면 401 권한 없음 오류가 발견됩니다.
{: tsSymptoms}

비활동 시간 **8시간**이 경과하면 브라우저 콘솔 세션의 제한시간이 초과됩니다. 세션이 비활성화되면 비활성 사용자는 콘솔에서 어떠한 조치도 수행할 수 없습니다.
{: tsCauses}

세션이 비활성화되면 브라우저를 새로 고쳐 보십시오. 작동하지 않을 경우 **모든** 탭과 창을 포함한 브라우저를 닫으십시오. URL을 다시 여십시오. 로그인해야 합니다. 

우수 사례로, 인증서와 ID를 이미 파일 시스템에 저장했을 수 있습니다. 익명 창을 사용하는 경우 브라우저를 닫으면 모든 인증서가 브라우저의 로컬 스토리에서 삭제됩니다. 다시 로그인한 후에 ID와 인증서를 다시 가져와야 합니다.
{: note}
