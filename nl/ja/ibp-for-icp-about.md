---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-23"

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

# {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private について
{: #ibp-icp-about}

{{site.data.keyword.blockchainfull}} Platform は、{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private をリリースしました。これは、コンテナー化されたアプリケーションを開発および管理するためのアプリケーション・プラットフォームです。 {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private オファリングは Kubernetes をベースとしています。そのため、ユーザーは、認証局 (CA)、順序付けプログラム、ピアを x86、LinuxONE、IBM Z にデプロイできます。{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、Kubernetes Helm チャートを使用してデプロイできます。
{:shortdesc}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、2019 年 4 月 23 日に Hyperledger Fabric v1.4.0 にアップグレードされます。ただし、現時点では、ゴシップ・データや個人データがサポートされる予定はありません。
{:note}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、{{site.data.keyword.cloud_notm}} Private を使用して独自のインフラストラクチャーでブロックチェーン・ネットワークを実行するために必要なコンポーネントを提供します。 コンポーネントには、Kubernetes Helm チャートを使用してデプロイ、管理、セットアップする Hyperledger Fabric、認証局 (CA)、順序付けプログラム、およびピアが含まれます。 **このオファリングは、Hyperledger Fabric の経験が豊富なお客様を対象としています。**

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private を使用すると、ブロックチェーン・ネットワークをプライベート・クラウドにデプロイして、データ常駐要件、市場規則、およびインフラストラクチャー設定に対応できます。 コンテナー化されたオンプレミス・アプリケーションを開発および管理するための Kubernetes ベースのアプリケーション・プラットフォームである {{site.data.keyword.cloud_notm}} Private を介して、独自のインフラストラクチャー内のブロックチェーン・ネットワークの重要な要素のデプロイメントを簡素化します。

 * クライアントが独自のインフラストラクチャーを使用して {{site.data.keyword.blockchainfull_notm}} Platform ネットワークを管理できるようにします。 無料の Community Edition では、お客様は独自の隔離されたセキュア環境で実行できますが、サポートは提供されません。
 * クライアントが Helm チャートと操作に関する詳細な資料を使用して Kubernetes 上で Fabric を構成できるようにします。
 * Community Edition を使用している場合を除き、クライアントに拡張テクニカル・サポートを提供します。

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、{{site.data.keyword.cloud_notm}} Private のお客様がブロックチェーン・コンポーネントをローカル環境にデプロイするためのバンドル製品です。 Helm チャートをインポートすると、{{site.data.keyword.cloud_notm}} Private カタログに {{site.data.keyword.blockchainfull_notm}} Platform タイルとして表示されます。 {{site.data.keyword.cloud_notm}} Private について詳しくは、[{{site.data.keyword.cloud_notm}} Private バージョン 3.1.2 ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/kc_welcome_containers.html "{{site.data.keyword.cloud_notm}} Private 3.1.2") の資料を参照してください。

## {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private の提供内容

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private では、Hyperledger Fabric ブロックチェーンのすべての基礎コンポーネント (認証局、順序付けサービス、およびピア) をデプロイできます。 これにより、ビジネス・ニーズに応じて、さまざまなコンポーネントを柔軟にデプロイできます。 {{site.data.keyword.blockchainfull_notm}} for {{site.data.keyword.cloud_notm}} Private を使用すると、組織をブロックチェーン共同事業体にバインドする順序付けサービスをデプロイおよび構成することにより、ブロックチェーン・ネットワークを開始できます。 また、ピアをデプロイし、Fabric に基づくコンポーネントを使用するその他のネットワーク ({{site.data.keyword.cloud_notm}} Private を使用してクラウド間にデプロイされた {{site.data.keyword.blockchainfull_notm}} Platform ネットワークや、IBM Cloud でホストされているスターター・プラン・ネットワークおよびエンタープライズ・プラン・ネットワークなど) に参加することもできます。 Hyperledger Fabric ネットワークのビルディング・ブロックについて詳しくは、[ブロックチェーン・コンポーネントの概要](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview)を参照してください。

## {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private の使用に適した状況

{{site.data.keyword.cloud_notm}} 外部で {{site.data.keyword.blockchainfull_notm}} Platform コンポーネントを実行すると、ブロックチェーン・ネットワークの拡張や参加をより柔軟に行うことができます。 これを使用すると、新規メンバーが各自のプラットフォームを使用したまま参加できるようになるので、ネットワーク・イニシエーターはネットワークの拡張を促進できます。これにより、ブロックチェーン・ネットワークへの参加に関心のある組織は、ピアを既存のアプリケーションと同じ場所に置いたり、組織の記録システムと統合したりできます。

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private をデプロイするプロセスは複雑であり、Fabric について高度な専門知識があることを想定しています。 Fabric、{{site.data.keyword.cloud_notm}} Private、または {{site.data.keyword.blockchainfull_notm}} Platform を使用するのが初めてで、開発環境や PoC (概念検証) の設定が目標である場合は、代わりに[スターター・プラン](/docs/services/blockchain/starter_plan.html#starter-plan-about)を使用することを検討してください。 また、すべての潜在的なデプロイメント構成が {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private でサポートされるわけではないことにも注意してください。
{:improtant}

このオファリングのユーザーは、独自のセキュリティーとインフラストラクチャーを管理することになります。 {{site.data.keyword.cloud_notm}} では、これらのサービスは提供されません。 開始する前に、次のセクションの[考慮事項と制限](/docs/services/blockchain/ibp-for-icp-about.html#ibp-icp-about-considerations)を確認してください。

## 考慮事項と制限
{: #ibp-icp-about-considerations}

開始する前に、以下の**考慮事項**と**制限**を理解していることを確認します。

- コンポーネントの正常性モニター、セキュリティー、ロギング、およびリソース使用量は、ユーザーが管理する必要があります。
- 他のクラウド環境で実行されているコンポーネントは、{{site.data.keyword.cloud_notm}} 上で実行中のネットワークのネットワーク・モニターに表示されません。
- Helm チャートは、順序付けプログラム、ピア、または CA の単一インスタンスをデプロイします。
- コンポーネントのリリース名が異なる場合、複数のコンポーネントを {{site.data.keyword.cloud_notm}} Private 内の単一の名前空間にデプロイできます。
- ネットワーク・モニター UI で Swagger UI を使用してコンポーネントをアドレス指定することはできません。
- 相互 TLS はサポートされていません。
- 基礎になっているテクノロジー (Hyperledger Fabric) では、コンテナーを使用してチェーンコードを実行し、Docker を使用してそのコンテナーを開始します。 ピアがチェーンコード・コンテナーを開始する唯一の方法は、Docker-in-Docker を使用することです。そのためには、特権アクセスが必要になります。

**CA に関する考慮事項**
- この Helm チャートは、CA の単一インスタンスをデプロイします。 組織ごとに個別の CA を設定することがベスト・プラクティスであると考えられるため、複数の CA をデプロイすることが必要になる場合があります。 例えば、1 つの順序付けプログラムと 3 つのピアをデプロイする予定である場合、少なくとも 2 つの CA が必要になります (順序付けプログラム組織用とピア組織用にそれぞれ 1 つずつ)。
- 別の MySQL データベースを実行することもできますが、Helm チャートにはこのオプションはありません。 ただし、Helm チャートでは、CA 内に SQLite データベースをデプロイして、ユーザーあたりのエンロール数や失効した証明書を記録するなどの CA のデータベース作業を処理します。

**順序付けプログラムに関する考慮事項**
- 順序付けサービスは、Hyperledger Fabric の v1.1 以降のすべてのコンポーネントと互換性があります。
- この Helm チャートは、SOLO 順序付けサービス (1 つの順序付けプログラム) の単一インスタンスをデプロイします。 順序付けサービスの可用性を高めるために、チャネル上に複数の SOLO 順序付けプログラムをデプロイすることはできません。 これは、SOLO 順序付けサービスが実動環境用ではなく開発環境用であると見なされる 1 つの理由です。 ただし、SOLO 順序付けサービスの複数のインスタンスを異なるネットワーク (つまり、別個の共同事業体) にデプロイできます。

**ピアに関する考慮事項**

- ピアは Fabric レベル v1.1 以降のブロックチェーン・ネットワークにのみ接続できます。 Hyperledger Fabric のバージョンを確認するには、ネットワーク・モニターで[「ネットワーク設定 (Network Preferences)」ウィンドウ](/docs/services/blockchain/v10_dashboard.html#ibp-dashboard-network-preferences)を開きます。 [手順](/docs/services/blockchain/v10_dashboard.html#ibp-dashboard-peer-connection-information)に従って、スターター・ネットワークまたはエンタープライズ・ネットワークからピア接続情報を取得します。
- ピアのデータベース・タイプがブロックチェーン・ネットワークのデータベース・タイプと一致する必要があります (LevelDB または CouchDB)。
- CouchDB Fauxton インターフェースは、ピアでは使用できません。
- ピアの[ゴシップ](/docs/services/blockchain/glossary.html#glossary-gossip)は現在サポートされていません。 これは、[プライベート・データ ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data-arch.html "プライベート・データ") や [サービス・ディスカバリー ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html "サービス・ディスカバリー") などのゴシップに依存する Fabric 機能もサポートされていないことを意味します。

## システム前提条件
{: #ibp-icp-about-prerequisites}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private では、以下のオペレーティング・システムがサポートされています。
- Red Hat Enterprise Linux (RHEL) 7.3、7.4、7.5
- Ubuntu 18.04 LTS および 16.04 LTS
- SUSE Linux Enterprise Server (SLES) 12 SP3

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private Helm チャートは、以下のワーカー・ノードおよび補助ストレージを使用して、Ubuntu Linux 上の {{site.data.keyword.cloud_notm}} Private v3.1.2 クラスターで稼働することが検証されました。

- **LinuxONE および IBM Z**: NFS を使用する z/VM および KVM
- **x86**: GlusterFS を使用する Linux 64 ビット

## ライセンスおよび料金
{: #ibp-icp-about-license-pricing}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、パスポート・アドバンテージからダウンロード可能な有料のオファリングと [GitHub ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://github.com/IBM/charts/tree/master/stable/ibm-blockchain-platform-dev "IBM/charts") で入手可能な無料の Community Edition の 2 つのエディションで構成されています。

### 使用許諾条件
{: #ibp-icp-about-license}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、独自のインフラストラクチャーでブロックチェーン・ネットワークを実行するために必要なコンポーネントを提供しており、{{site.data.keyword.cloud_notm}} Private アプリケーションとしてデプロイされます。 PPA にアクセスして、[Helm チャートをダウンロード](/docs/services/blockchain/howto/helm_install_icp.html#helm-install)できます。 {{site.data.keyword.blockchainfull_notm}} からの技術サポートが購入内容に含まれています。

{{site.data.keyword.blockchainfull_notm}} Platform for IBM Cloud Private Community Edition は、評価および試験に適した無料のオファリングであり、{{site.data.keyword.cloud_notm}} Private アプリケーションとしてデプロイされます。 実動には、Community Edition を使用しないでください。 {{site.data.keyword.blockchainfull_notm}} Platform では、Community Edition をサポートしていません。 [GitHub パッケージ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://github.com/IBM/charts/blob/master/repo/stable/ibm-blockchain-platform-dev-1.0.2.tgz "IBM/charts") にアクセスし、Helm チャートをダウンロードできます。

### 料金
{: #ibp-icp-about-pricing}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private の料金は、使用される仮想プロセッサー・コア (VPC) の数に基づきます。 VPC は、仮想サーバーに割り当てられた仮想コアか、非パーティション化サーバーの物理プロセッサー・コアのいずれかです。 {{site.data.keyword.blockchainfull_notm}} Platform で使用可能な VPC ごとに、ライセンス交付を受けた使用権を取得する必要があります。<!-- A VPC is a unit of measurement by which a program can be licensed.-->

VPC の使用法の判別方法について詳しくは、{{site.data.keyword.IBM_notm}} Knowledge Center の [Virtual Processor Cores (VPC) ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SS8JFY_9.2.0/com.ibm.lmt.doc/Inventory/overview/c_virtual_processor_core_licenses.html "Virtual Processor Cores (VPC's)") に関するこの記事を参照してください。 [{{site.data.keyword.IBM_notm}} License Metric Tool](https://www.ibm.com/support/knowledgecenter/en/SS8JFY_9.2.0/com.ibm.lmt.doc/welcome/LMT_welcome.html) を使用して、ライセンスを取得するために必要な VPC の数を判別するために使用できるレポートを構成および作成できます。


## {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private のインストール
{: #ibp-icp-about-install}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、ローカル {{site.data.keyword.cloud_notm}} Private クラスターにインストール可能な Helm チャート・ファイルとして提供されます。Helm チャートをインストールすると、{{site.data.keyword.cloud_notm}} Private カタログで {{site.data.keyword.blockchainfull_notm}} Platform をアプリケーションとして見つけることができます。

- {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private は、パスポート・アドバンテージによって提供されます。 [パスポート・アドバンテージ・オンライン](https://www.ibm.com/software/passportadvantage/pao_customer.html)にアクセスするには、そのためのライセンスが必要です。 購入内容には、{{site.data.keyword.blockchainfull_notm}} Platform の技術サポートが含まれています。

- {{site.data.keyword.blockchainfull_notm}} Platform Community Edition は、探索、開発、およびテスト用です。 この {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private の無料バージョンには、GitHub からアクセスできます。 **注:** {{site.data.keyword.blockchainfull_notm}} Platform では、Community Edition をサポートしていません。

Helm チャートのインストール方法に関する手順および必要な前提条件については、[{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private のインストール](/docs/services/blockchain/howto/helm_install_icp.html#helm-install)を参照してください。

{{site.data.keyword.cloud_notm}} Private の新規ユーザーであり、{{site.data.keyword.cloud_notm}} Private のインストールおよびデプロイに関する情報とヒントが必要な場合は、[{{site.data.keyword.cloud_notm}} Private のセットアップ](/docs/services/blockchain/ICP_setup.html#icp-setup)を参照してください。

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private をインストールした後、ネットワークの各コンポーネント個別にデプロイする必要があります。 一度に複数のコンポーネントをデプロイすることはできません。 ブロックチェーン・ネットワークの構築またはブロックチェーン・ネットワークへの参加のためのベスト・プラクティスについては、[{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private の概説](/docs/services/blockchain/ibp_for_icp_deployment_guide.html#get-started-icp)を参照してください。その後、以下のセクションで、個別のコンポーネントをデプロイおよび操作するためのステップを確認します。

### ファイアウォールの内側での {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private のインストール
{: #ibp-icp-about-firewall}

パブリック・インターネットへのアクセス権限がなくても、ファイアウォールの内側に {{site.data.keyword.blockchainfull_notm}} Platform コンポーネントをデプロイできます。 ダウンロードされた Helm チャート・パッケージには、{{site.data.keyword.blockchainfull_notm}} Platform で使用するすべての Fabric コンポーネントの Docker イメージが、デプロイメント時に DockerHub からプルされることなく含まれます。

{{site.data.keyword.blockchainfull_notm}} Platform Community Edition Helm チャート・パッケージには、必要な Fabric コンポーネントの Docker イメージは含まれません。 これは、デプロイメント時に DockerHub からこれらのイメージをダウンロードするように構成され、パブリック・インターネットへのアクセス権限がない場合には失敗します。 ただし、いくつかの追加ステップを実行して、Community Edition コンポーネントをファイアウォールの内側にデプロイできます。 詳しくは、[ファイアウォールの内側での Community Edition のインストール](/docs/services/blockchain/howto/helm_install_icp.html#helm-install-prereqs-firewall)を参照してください。


## {{site.data.keyword.cloud_notm}} Private の認証局について
{: #ibp-icp-about-ca}

認証局 (CA) は、ネットワーク上の ID を提供します。 CA は、複数の団体の間でトラスト・アンカーとしての役割を果たす、公証人のようなものと考えることができます。 ネットワーク内のすべてのエンティティーに、各自のデジタル ID が組み込まれた証明書が、ルート CA の署名付きで付与されます。 この証明書が、ネットワーク上で実行されるすべての署名操作と検証操作のトラスト・ルートです。 認証局およびそれらがブロックチェーン・ネットワークで果たす役割について詳しくは、[ブロックチェーン・コンポーネントの概要](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview)を参照してください。

CA は、ID を検証し、デプロイする必要があるネットワーク内の他のコンポーネントについて証明書を発行します。 そのため、他のコンポーネントをデプロイする前に、組織の CA をデプロイする必要があります。

- Helm チャートのインストール後に CA を構成およびデプロイする方法については、[{{site.data.keyword.cloud_notm}} Private への認証局のデプロイ](/docs/services/blockchain/howto/CA_deploy_icp.html#ca-deploy)を参照してください。

- CA を使用して証明書を生成し、追加コンポーネントをデプロイするための前提条件ステップを実行する方法については、[{{site.data.keyword.cloud_notm}} Private での認証局の操作](/docs/services/blockchain/howto/CA_operate.html#ca-operate)を参照してください。

## {{site.data.keyword.cloud_notm}} Private の順序付けプログラムについて
{: #ibp-icp-about-orderer}

順序付けプログラムは、ブロックチェーン・ネットワーク内のクライアント、順序付けトランザクション、およびブロードキャスト・トランザクションを認証します。 これらは、Hyperledger Fabric に基づくブロックチェーン・ネットワークの共通バインディングです。 そのため、他の組織がピアをデプロイし、チャネルに参加して、ネットワーク上でトランザクションを開始できるようにするには、まず、ネットワークを構築する組織が、「順序付けサービス」(順序付けを行うノードまたはノードの集合) をデプロイして開始する必要があります。 順序付けプログラムと、ブロックチェーン・ネットワーク内でのその役割について詳しくは、[ブロックチェーン・コンポーネントの概要](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview-orderer)を参照してください。

ブロックチェーン・ネットワークを構築する場合、順序付けプログラムをデプロイする必要があります。 順序付けプログラムをデプロイした後、他の組織を共同事業体に招待してから、共同事業体で独自のチャネルを作成できます。

- Helm チャートのインストール後に順序付けプログラムを構成してデプロイする方法については、[{{site.data.keyword.cloud_notm}} Private への順序付けプログラムのデプロイ](/docs/services/blockchain/howto/orderer_deploy_icp.html#icp-orderer-deploy)を参照してください。

- 共同事業体の構築方法については、[{{site.data.keyword.cloud_notm}} Private での順序付けプログラムの操作](/docs/services/blockchain/howto/orderer_operate.html#icp-orderer-operate)を参照してください。

## {{site.data.keyword.cloud_notm}} Private のピアについて
{: #ibp-icp-about-peer}

ピアは、台帳およびスマート・コントラクトをホストするため、ネットワークの基本的な要素です。 スマート・コントラクトおよび台帳は、ネットワークで共有プロセスおよび共有情報をそれぞれカプセル化するために使用されます。 ピアおよびそれらがブロックチェーン・ネットワークで果たす役割について詳しくは、[ブロックチェーン・コンポーネントの概要](/docs/services/blockchain/blockchain_component_overview.html#blockchain-component-overview)を参照してください。

- ネットワークに参加する準備ができたら、チャネルに参加してトランザクションを承認し、チャネル台帳を保管するピアをデプロイできます。 {{site.data.keyword.cloud_notm}} Private 上の他のコンポーネントに接続するピアを {{site.data.keyword.cloud_notm}} Private にデプロイする方法について詳しくは、[{{site.data.keyword.cloud_notm}} Private でのピアのデプロイ](/docs/services/blockchain/howto/peer_deploy_icp.html#icp-peer-deploy)を参照してください。 スターター・プラン・ネットワークまたはエンタープライズ・プラン・ネットワークに接続するピアを {{site.data.keyword.cloud_notm}} Private にデプロイする方法について詳しくは、[スターターまたはエンタープライズに接続するピアのデプロイ](/docs/services/blockchain/howto/peer_deploy_ibp.html#ibp-peer-deploy)を参照してください。

- ピアをセットアップした後、トランザクションを送信し、ブロックチェーン・ネットワークからの分散台帳を読み取るには、いくつかの操作ステップを完了する必要があります。

  - {{site.data.keyword.cloud_notm}} Private にデプロイされた {{site.data.keyword.blockchainfull_notm}} Platform にピアを接続する場合は、[マルチクラウド・ネットワークを使用した {{site.data.keyword.cloud_notm}} Private でのピアの操作](/docs/services/blockchain/howto/peer_operate_icp.html#icp-peer-operate)を参照してください。
  - {{site.data.keyword.cloud_notm}} にデプロイされたスターター・プラン・ネットワークまたはエンタープライズ・プラン・ネットワークにピアを接続する場合は、[スターター・プランまたはエンタープライズ・プランを使用した {{site.data.keyword.cloud_notm}} Private でのピアの操作](/docs/services/blockchain/howto/peer_operate_ibp.html#ibp-peer-operate)を参照してください。

## セキュリティーに関する考慮事項
{: #ibp-icp-about-security}

これらのコンポーネントは {{site.data.keyword.cloud_notm}} 外部にデプロイされるため、そのセキュリティーはユーザーが管理する必要があります。 これには、鍵管理やデータ暗号化など、セキュリティーの重要な領域が含まれます。 コンポーネントのセキュリティーを考慮する場合は、以下のトピックを確認してください。

### データ・セキュリティー
{: #ibp-icp-about-security-data}

{{site.data.keyword.blockchainfull_notm}} Platform のスターター・プランおよびエンタープライズ・プランでは、[対称鍵暗号 ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSB23S_1.1.0.14/gtps7/s7symm.html "対称暗号方") に基づくディスク全体の暗号化を使用して、ネットワークで使用されるすべてのデータを保護します。 ご使用の環境でも同様のステップを実行して、ピア・データを保護する必要があります。

状態データベース内のデータは、LevelDB と CouchDB のどちらを使用するかに関係なく、暗号化されません。 アプリケーション・レベルの暗号化によって、状態データベースに保管されているデータを保護できます。

### データの常駐
{: #ibp-icp-about-security-data-residency}

データの常駐要件により、すべてのブロックチェーン台帳データの処理および保管を 1 つの国 (または定義された他の境界内) にとどめることを義務付けることができます。 データの常駐の実現方法について詳しくは、[データの常駐](#ibp-icp-about-data-residency)を参照してください。

### 鍵管理
{: #ibp-icp-about-security-key-management}

鍵管理はセキュリティーの重要な側面です。 秘密鍵が漏えいしたり、失われたりすると、悪意を持つアクターがデータおよび機能にアクセスできる可能性があります。 IBM では、[ハードウェア・セキュリティー・モジュール](/docs/services/blockchain/glossary.html#glossary-hsm) (HSM) と呼ばれる物理アプライアンスを使用して、{{site.data.keyword.blockchainfull_notm}} Platform エンタープライズ・プラン・ネットワークの秘密鍵を保管します。

{{site.data.keyword.cloud_notm}} Private にコンポーネントをデプロイする場合は、ユーザーが秘密鍵を管理する必要があります。 {{site.data.keyword.blockchainfull_notm}} Platform によって秘密鍵が生成されますが、鍵は Platform には保管されません。 鍵が漏えいしないように、鍵を安全に保管することが重要です。 コンポーネントの秘密鍵は、ピア MSP の keystore フォルダー (コンポーネント内の `/mnt/crypto/peer/peer/msp/keystore/` ディレクトリー) にあります。 ピア内部の証明書について詳しくは、[{{site.data.keyword.blockchainfull_notm}} Platform の証明書の管理](/docs/services/blockchain/certificates.html#managing-certificates)のチュートリアルの[メンバーシップ・サービス・プロバイダー](/docs/services/blockchain/certificates.html#managing-certificates-msp)のセクションを参照してください。

鍵エスクローを使用して、失われた秘密鍵を復旧することができます。 これは、鍵が失われる前に実行する必要があります。 秘密鍵を復旧できない場合は、認証局に新しい ID を登録して、新しい秘密鍵を取得する必要があります。 また、参加しているチャネルから signCert を削除し、置き換える必要があります。

### TLS
{: #ibp-icp-about-security-tls}

[Transport Layer Security![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10660_.htm "SSL または TLS ハンドシェークの概要") (TLS) は、Hyperledger Fabric の信頼モデルに組み込まれています。 {{site.data.keyword.blockchainfull_notm}} Platform のすべてのスターター・コンポーネントとエンタープライズ・コンポーネントでは、TLS を使用して認証し、相互に通信します。 したがって、Platform のネットワーク・コンポーネントは、ピアとの TLS ハンドシェークを実行できる必要があります。 これに関連して、ホワイト・リストなどを使用して、クライアント・アプリからピアまでファイアウォールでパススルーできる必要があります。

### メンバーシップ・サービス・プロバイダーの構成
{: #ibp-icp-about-security-MSP}

{{site.data.keyword.blockchainfull_notm}} Platform のコンポーネントは、メンバーシップ・サービス・プロバイダー (MSP) を介して ID を使用します。 MSP は、CA から発行された証明書をネットワークおよびチャネルの役割に関連付けます。 MSP がピアを使用する方法について詳しくは、[メンバーシップ・サービス・プロバイダー (MSP)](/docs/services/blockchain/certificates.html#managing-certificates-msp) を参照してください。

### アプリケーション・セキュリティー
{: #ibp-icp-about-security-appl}

すべてのチェーンコード呼び出しは署名されているため、Fabric によってアプリケーション・セキュリティーが管理されます。 また、Fabric には ACL ベースのアプリケーション・レベル・チェックも含まれています。

## データの常駐
{: #ibp-icp-about-data-residency}

ブロックチェーン・ネットワークでは、処理されるデータのタイプが認識されないため、特定の種類のデータを保護するために追加のステップが必要になる場合があります。 データの常駐に関する最も一般的な要件は、IT システムで処理および保管されるすべてのデータを特定の国の中にとどめることを義務付ける、特定の国の法律に関連付けられています。 同様に、政府、医療、金融サービスなど、規制の厳しい業界の企業は、データを完全にファイアウォールの内側に保管することが求められます。 したがって、データの常駐を実現するには、ブロックチェーン・ネットワークのすべてのコンポーネントが同じ[チャネル](/docs/services/blockchain/glossary.html#glossary-channel)の一部であり、1 つの国に常駐する必要があります。

データの常駐要件に対応するには、{{site.data.keyword.blockchainfull_notm}} Platform の基礎となっている Hyperledger Fabric アーキテクチャーを理解することが重要です。 このアーキテクチャーは、順序付けサービス (順序付けプログラムで構成)、認証局 (CA)、およびピアという 3 つの主要コンポーネントを中核としています。 ピアは順序付けサービスから順序付け状態の更新をブロックの形式で受け取り、状態および台帳を維持します。 したがって、ピアと順序付けサービスには直接的な関係があります。 台帳には、トランザクション・ログに含まれるすべてのキーおよびデータの最新の値が含まれます。

さらに、クライアント・アプリケーションは、[Fabric SDK](/docs/services/blockchain/v10_application.html#dev-app-fabric-sdks) を使用してトランザクションをピアおよび順序付けサービスに送信します。 これらのトランザクションには、台帳のキーと値のペアを含む[読み取り/書き込みセット ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/readwrite.html "読み取り/書き込みセットのセマンティクス") のデータが含まれます。

データの国内常駐が要件となっている場合、順序付けプログラム、ピア、およびクライアント・アプリケーションが同じ国に常駐する必要があります。 {{site.data.keyword.blockchainfull_notm}} Platform ネットワークが {{site.data.keyword.cloud_notm}} で作成されている場合、ネットワークのロケーションを選択することができます。 <!--For a Starter Plan network, you can select from US South, United Kingdom, and Sydney. For an Enterprise Plan network, you can select from currently available locations, which include Dallas, Frankfurt, London, Sao Paulo, Tokyo, and Toronto. -->地域とロケーションについて詳しくは、[{{site.data.keyword.blockchainfull_notm}} Platform の地域とロケーション](/docs/services/blockchain/reference/ibp_regions.html#ibp-regions-locations)を参照してください。

### データの常駐のユース・ケース

4 つの組織の共同事業体とともに順序付けプログラムと CA を含む {{site.data.keyword.blockchainfull_notm}} Platform ネットワークを考えてみましょう。 組織には 1 つ以上のピア・ノードがあり、4 つの組織はすべて単一チャネルの一部で、ネットワークのすべてのコンポーネントは {{site.data.keyword.blockchainfull_notm}} Platform ネットワークがデプロイされた地域に常駐します (フランクフルトなど)。 最後に、ピアと相互動作するクライアント・アプリケーションもドイツ内にあります。

この例では、データの常駐は維持されます。

![すべてのコンポーネントが同じ国内に存在する場合のデータの常駐](images/remote_peer_data_res_1.png "すべてのコンポーネントが同じ国内に存在する場合のデータの常駐")
*図 1. すべてのコンポーネントが同じ国内に存在する場合のデータの常駐*

ここで、**分散ピア**がいずれかの組織に参加した場合の影響について考えてみましょう。 分散ピアは、ネットワークの他の部分と同じ地域に常駐することも、{{site.data.keyword.blockchainfull_notm}} Platform ネットワークの地域外の任意の場所に常駐することもできます。

-	このピアがネットワークの残り部分と同じ国にある場合は、データの常駐は維持されます。 上記の**図 1** のように、すべての台帳データはドイツ内にとどまります。
-	このピアが別の国 (米国など) に存在する場合は、ピア台帳上のデータは国境にまたがって共有されるため、データの常駐は維持されなくなります。

この問題を解決するために、**チャネル**を使用してネットワーク上のピアのサブセットに対してデータを分離できます。 {{site.data.keyword.blockchainfull_notm}} Platform ネットワークに、国をまたぐ分散ピアおよび順序付けプログラムが含まれる場合、チャネルを使用して、国外のピアを含む組織から元帳データを分離できます。

**注:** 順序付けプログラムは常に、ネットワークをホストするように選択したデータ・センターの地域に配置されます。 国境にまたがる複数の順序付けプログラムを保持することはできません。 ただし、ピアは、データ・センターと {{site.data.keyword.cloud_notm}} の外側のリモート・ロケーションのいずれにも配置できます。

![ピアが {{site.data.keyword.blockchainfull_notm}} Platform の地域の国外に存在する場合のデータの所在場所](images/remote_peer_data_res_2.png "ピアが {{site.data.keyword.blockchainfull_notm}} Platform の地域の国外に存在する場合のデータの所在場所")
*図 2. ピアが {{site.data.keyword.blockchainfull_notm}} Platform の地域の国外に存在する場合のデータの所在場所*

**図 2** では、`OrgC` および `OrgD` にデータの常駐は必要ありません。 実際、`OrgD` には現在、*米国*に常駐する `OrgD-peer1` と `OrgD-peer2` の 2 つの分散ピアが含まれています。 したがって、`OrgA`、`OrgB`、およびドイツに常駐するそれぞれのクライアント・アプリケーションとピアがチャネル `X` の元帳データを分離できるように、新規チャネル `Y` が `OrgC` および `OrgD` 用に作成されます。

{{site.data.keyword.blockchainfull_notm}} Platform ネットワーク上のデータのフローについて詳しくは、[トランザクション・フローに関する Fabric の資料 ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/txflow.html "Transaction Flow") を参照してください。

今後、Hyperledger Fabric の新しいテクノロジーによって、[プライベート・データ・コレクション ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data/private-data.html "プライベート・データ・コレクション") およびゼロ知識証明を使用して、さらなるデータの常駐を実現する機能が改善されます。

- プライベート・データ・コレクションによって、プライベート・データが、国内のピアなど、表示を許可されたピアにのみピアツーピアで共有されます (ゴシップ・プロトコルによって)。 データはピアのプライベート・データベースに保管されます。 順序付けサービスは、ここでは関与しません。またプライベート・データを認識することもありません。 チャネルのすべてのピアの台帳にこのデータのハッシュが書き込まれます。 状態検証で使用されるハッシュは、トランザクションの証拠として機能し、監査目的で使用することができます。 プライベート・データは、Fabric バージョン 1.2.1 以降上で稼働している {{site.data.keyword.blockchainfull_notm}} Platform 上のネットワークで使用できます。 ただし、{{site.data.keyword.cloud_notm}} Private ネットワークでは現在ゴシップを使用していないため、{{site.data.keyword.cloud_notm}} Private で実行されているピアに対してプライベート・データ機能を使用することはできません。

- ゼロ知識証明 (ZKP) により、「証明者」は「検証者」に、機密事項自体を示すことなく、機密事項に関する知識があることを保証できます。

これらのテクノロジーについて詳しくは、[Hyperledger Fabric を使用したプライベートおよび機密トランザクション ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://developer.ibm.com/tutorials/cl-blockchain-private-confidential-transactions-hyperledger-fabric-zero-knowledge-proof/ "Hyperledger Fabric を使用したプライベートおよび機密トランザクション") に関するホワイト・ペーパーを参照してください。

## サポートについて
{: #ibp-icp-about-support}

デジタル・サポート・オファリングについて詳しくは、{{site.data.keyword.blockchainfull_notm}} Platform サポートの[リソースおよびサポート・フォーラム](/docs/services/blockchain/ibmblockchain_support.html#blockchain-support-resources)を参照してください。

### {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private ライセンスを購入し、お客様サポートに連絡する場合は、[IBM Support Community へのアクセスおよびサポート・チケットのオープン ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://www-01.ibm.com/support/docview.wss?uid=ibm10740041 "{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private Support") を参照してください。

### {{site.data.keyword.blockchainfull_notm}} Platform Community Edition

Community Edition は探索、開発、およびテストを目的としたものです。 {{site.data.keyword.blockchainfull_notm}} Platform では、{{site.data.keyword.blockchainfull_notm}} Platform Community Edition をサポートしていません。

ブロックチェーン・コンポーネントに関連する問題が発生した場合は、無料のブロックチェーン開発者リソースとサポート・フォーラムを使用して、IBM および Fabric コミュニティーから支援を受けることができます。 詳しくは、[ブロックチェーンのリソースおよびサポート・フォーラム](/docs/services/blockchain/ibmblockchain_support.html#blockchain-support-resources)を参照してください。

IBM Cloud Private に関連する問題の場合は、[無料デジタル・サポートと {{site.data.keyword.cloud_notm}} Private が提供する有料サポート](https://www.ibm.com/developerworks/community/blogs/fe25b4ef-ea6a-4d86-a629-6f87ccf4649e/entry/Learn_more_about_IBM_Cloud_Private_Support?lang=en_us)の両方をご利用できます。
