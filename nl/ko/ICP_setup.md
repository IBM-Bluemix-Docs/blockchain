---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-16"

keywords: IBM Cloud Private, data storage CA, cluster ICP, configuration

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

# {{site.data.keyword.cloud_notm}} Private 설정
{: #icp-setup}

{{site.data.keyword.cloud_notm}} Private에 {{site.data.keyword.blockchainfull}} Platform 컴포넌트를 배치하고 블록체인 네트워크를 빌드하려면 먼저 사용자 환경에서 {{site.data.keyword.cloud_notm}} Private을 설정해야 합니다.
{:shortdesc}

## 전제조건
{: #icp-setup-prerequisites}

다음 전제조건을 완료한 후 {{site.data.keyword.cloud_notm}} Private을 설치할 환경을 준비하십시오.

### Docker
{{site.data.keyword.cloud_notm}} Private을 사용하려면 Docker가 설치되어 있어야 합니다. [{{site.data.keyword.cloud_notm}} Private 설치 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/installing/install.html "{{site.data.keyword.cloud_notm}} Private 설치")의 지시사항에 따라 Docker를 설치하십시오.

### {{site.data.keyword.cloud_notm}} Private 설정
{{site.data.keyword.cloud_notm}} Private을 설치하기 전에 {{site.data.keyword.cloud_notm}} Private 설치에 필요한 노드를 준비하기 위해 다음과 같은 팁이 유용합니다. 추가적인
{{site.data.keyword.cloud_notm}} Private 전제조건은 [{{site.data.keyword.cloud_notm}} Private 문서 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/installing/prep.html "설치할 클러스터 준비")에서 찾을 수 있습니다.

#### `vm.max_map_count` 설정 업데이트
{{site.data.keyword.cloud_notm}} Private은 로깅 및 측정을 위해 Elastic Search를 사용합니다. Elastic Search의 경우 메모리 부족 예외를 방지하기 위해 `vm.max_map_count` 시스템 특성이 구성되어 있어야 합니다. {{site.data.keyword.cloud_notm}} Private을 설치하기 전에 [Elastic Search 구성 지시사항 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html "가상 메모리")을 참조하여 각각의 노드에 이 특성을 구성하십시오. 다음 명령을 사용하여 영구적으로 이 특성을 설정할 수 있습니다.

```
sysctl -w vm.max_map_count=262144; sysctl vm.max_map_count
echo "vm.max_map_count=262144” | tee -a /etc/sysctl.conf
```
{:codeblock}

#### 클러스터에 있는 각각의 노드에 `/etc/hosts` 파일 구성

- {{site.data.keyword.cloud_notm}} Private은 [Kubernetes ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://kubernetes.io/docs/tutorials/kubernetes-basics/ "Kubernetes의 기본 사항 학습")를 사용하여 컨테이너화된 애플리케이션을 관리합니다. 각각의 노드에 있는 `/etc/hosts`에 호스트 이름이 구성되어 있지 않은 경우 Kubernetes 도메인 이름 서버(DNS)가 실패합니다. 각각의 노드에 있는 `/etc/hosts` 파일에 [클러스터에 있는 각각의 노드에 대한 IP 주소, 호스트 이름 및 단축 이름을 삽입![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/installing/prep_cluster.html "클러스터 구성")하십시오.

- [{{site.data.keyword.cloud_notm}} Private에서는 IPv6이 지원되지 않습니다 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/getting_started/known_issues.html#ipv6 "IPv6은 지원되지 않음"). {{site.data.keyword.cloud_notm}} Private 클러스터에서 DNS 서비스 관련 문제점을 방지하려면 각각의 노드에 있는 `/etc/hosts` 파일에서 다음 행의 시작 부분에 `#` 부호를 사용하여 해당 행을 주석 처리함으로써 IPv6 설정을 사용 안함으로 설정하십시오.
  ```
  #::1  localhost ip6-localhost ip6-loopback
  ```
  {:codeblock}

### 필수 리소스
{: #icp-setup-resources}

각 Fabric 런타임 컴포넌트마다 사용자의 {{site.data.keyword.cloud_notm}} Private 시스템이 최소 하드웨어 리소스 요구사항을 충족하는지 확인하십시오.

|컴포넌트 | vCPU | RAM | 데이터 스토리지용 디스크 |
|-----------|------|-----|-----------------------|
| CA |1 |192MB | 1GB |
| 순서 지정자 |2 | 512MB | 100GB(확장 기능 포함) |
| 피어 |2 |2GB | 50GB(확장 기능 포함) |
| 피어를 위한 CouchDB<br>(CouchDB를 사용하는 경우에만 적용 가능) |2|2GB | 50GB(확장 기능 포함) |

 **참고:**
 - vCPU는 서버가 가상 머신에 대해 파티션되지 않은 경우 가상 머신 또는 실제 프로세서 코어에 지정되는 가상 코어입니다. {{site.data.keyword.cloud_notm}} Private에서 배치를 위해 가상 프로세서 코어(VPC)를 결정할 때 vCPU 요구사항을 고려해야 합니다. VPC는 {{site.data.keyword.IBM_notm}} 제품의 라이센싱 비용을 판별하는 측정 단위입니다. VPC를 결정하는 시나리오에 대한 자세한 정보는 [가상 프로세서 코어(VPC) ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SS8JFY_9.2.0/com.ibm.lmt.doc/Inventory/overview/c_virtual_processor_core_licenses.html)를 참조하십시오.
 - 이 최소 리소스 레벨은 테스트 및 실험을 수행하는 데 충분합니다. 대량의 트랜잭션이 발생하는 환경의 경우 충분히 큰 스토리지 용량(예: 피어에 250GB 및 순서 지정 서비스에 500GB)을 할당하는 것이 중요합니다. 사용할 스토리지의 양은 네트워크에서 필요한 트랜잭션의 수와 서명의 수에 따라 달라집니다. 피어 또는 순서 지정자에서 스토리지를 다 써버리는 경우 대형 파일 시스템에서 새 피어 또는 순서 지정자를 배치해야 하고 동일한 채널의 기타 컴포넌트를 통해 동기화할 수 있도록 해야 합니다.

#### 스토리지 고려사항
{: #icp-setup-storage-considerations}

* 컴포넌트에서 사용할 스토리지를 판별해야 합니다. 기본 설정을 사용하는 경우 피어 Helm 차트에서 피어 데이터를 위해 이름이 `my-data-pvc`인 지속적 볼륨 청구를 작성합니다. 원장 데이터베이스로 CouchDB를 선택하는 경우 Helm 차트에서 원장 데이터베이스를 위해 이름이 `statedb-pvc`인 다른 지속적 볼륨 청구를 작성합니다.
* 기본 스토리지 설정을 사용하지 않으려면 {{site.data.keyword.cloud_notm}} Private 설치 중에 *새* storageClass가 설정되었는지 확인하거나, Kubernetes 시스템 관리자 배치하기 전에 storageClass를 작성해야 합니다.
* [동적 프로비저닝 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/ "동적 볼륨 프로비저닝")은 {{site.data.keyword.cloud_notm}} Private의 amd64 노드에서만 사용할 수 있습니다. 따라서 클러스터에 s390x 와 amd64 작업자 노드가 혼합되어 있는 경우 동적 프로비저닝을 사용할 수 없습니다.
* 동적 프로비저닝을 사용하지 않을 경우 [지속적 볼륨 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://kubernetes.io/docs/concepts/storage/persistent-volumes/ "지속적 볼륨")을 작성하여 Kubernetes 지속적 볼륨 청구(PVC) 바인드 프로세스를 세분화하기 위해 사용할 수 있는 레이블로 설정해야 합니다.
* NFS v2/v3 지속적 볼륨을 사용하는 경우 NFS 파일 시스템이 존재하는 호스트 시스템에서 **NFSv2/v3 파일 시스템 잠금을 위한 NFS 상태 모니터** 모듈(**rpc-statd**)을 사용으로 설정해야 합니다. 이 모듈은 NFS 파일 시스템에서 다른 프로세스가 보유한 파일에 대한 독점적 잠금을 확인할 수 있도록 해줍니다. 이 모듈을 사용으로 설정하려면 다음 명령을 실행하십시오.

  ```
  sudo systemctl enable rpc-statd
  ```
  {:codeblock}

  ```
  sudo systemctl start rpc-statd
  ```
  {:codeblock}

## {{site.data.keyword.cloud_notm}} Private 설치
{: #icp-setup-install}

사용자 환경에 {{site.data.keyword.cloud_notm}} Private을 설치 및 설정하려면 다음 단계를 완료하십시오.

1. [{{site.data.keyword.cloud_notm}} Private ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘") ](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/kc_welcome_containers.html) 클러스터 버전 3.1.2를 설치하십시오. 개발, 테스트 또는 시범용으로 Helm 차트를 사용하려는 경우 무료로 [{{site.data.keyword.cloud_notm}} Private Community Edition 버전 3.1.2 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/kc_welcome_containers.html "{{site.data.keyword.cloud_notm}} Private-CE 버전 3.1.2")를 설치할 수 있습니다.

2. CA를 설치하고 작동시키기 위해 {{site.data.keyword.cloud_notm}} Private CLI [3.1.2 ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/manage_cluster/install_cli.html)를 설치하십시오.

3. 대상 네임스페이스에 대한 팟(Pod) 보안 정책을 설정합니다. 지시사항은 [다음 절](#icp-setup-psp)에서 제공됩니다.

{{site.data.keyword.cloud_notm}} Private을 설치하고 팟(Pod) 보안 정책을 대상 네임스페이스에 바인드한 후에도 계속 {{site.data.keyword.cloud_notm}} Private 클러스터로 [{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private Helm 차트를 가져올](/docs/services/blockchain/howto/helm_install_icp.html#helm-install) 수 있습니다.

## PodSecurityPolicy 요구사항
{: #icp-setup-psp}

Helm 차트를 사용하여 컴포넌트를 배치하려면 새 대상 네임스페이스를 작성하고 [PodSecurityPolicy ![외부 링크 아이콘](images/external_link.svg "외부 링크 아이콘")](https://kubernetes.io/docs/concepts/policy/pod-security-policy/ "Pod Security Policies")를 네임스페이스에 바인드해야 합니다.  사전 정의된 PodSecurityPolicy를 선택하거나 클러스터 관리자가 사용자를 위해 사용자 정의 PodSecurityPolicy를 작성하도록 하십시오.
- 사전 정의된 PodSecurityPolicy 이름: [`ibm-privileged-psp`](https://ibm.biz/cpkspec-psp)
- 사용자 정의 PodSecurityPolicy 정의:
  ```
  apiVersion: extensions/v1beta1
  kind: PodSecurityPolicy
  metadata:
    name: ibm-blockchain-platform-psp
  spec:
    hostIPC: false
    hostNetwork: false
    hostPID: false
    privileged: true
    allowPrivilegeEscalation: true
    readOnlyRootFilesystem: false
    seLinux:
      rule: RunAsAny
    supplementalGroups:
      rule: RunAsAny
    runAsUser:
      rule: RunAsAny
    fsGroup:
      rule: RunAsAny
    requiredDropCapabilities:
    - ALL
    allowedCapabilities:
    - NET_BIND_SERVICE
    - CHOWN
    - DAC_OVERRIDE
    - SETGID
    - SETUID
    volumes:
    - '*'
  ```
  {:codeblock}
- 사용자 정의 PodSecurityPolicy를 위한 사용자 정의 ClusterRole:
  ```
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    annotations:
    name: ibm-blockchain-platform-clusterrole
  rules:
  - apiGroups:
    - extensions
    resourceNames:
    - ibm-blockchain-platform-psp
    resources:
    - podsecuritypolicies
    verbs:
    - use
  - apiGroups:
    - ""
    resources:
    - secrets
    verbs:
    - create
    - delete
    - get
    - list
    - patch
    - update
    - watch
  ```
  {:codeblock}

- 사용자 정의 ClusterRole을 위한 사용자 정의 ClusterRoleBinding:
  ```
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRoleBinding
  metadata:
   name: ibm-blockchain-platform-clusterrolebinding
  roleRef:
   apiGroup: rbac.authorization.k8s.io
   kind: ClusterRole
   name: ibm-blockchain-platform-clusterrole
  subjects:
  - kind: ServiceAccount
    name: default
    namespace: default
  ```
  {:codeblock}
