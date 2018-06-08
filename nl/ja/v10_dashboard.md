---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Enterprise Plan ネットワークの操作
{: #v10_dashboard}

{{site.data.keyword.blockchainfull}} Platform に用意されたネットワーク・モニターにはブロックチェーン環境の概要が示されるので、ネットワーク・リソース、メンバー、結合されたチャネル、トランザクション・パフォーマンス・データ、デプロイされたチェーンコードなどを把握できます。 また、ネットワーク・モニターにはエントリー・ポイントとしての役割もあり、そこから Swagger API を実行したり、{{site.data.keyword.blockchainfull_notm}} Platform: Develop を使用してネットワークを開発したり、サンプル・アプリケーションを試したりできます。
{:shortdesc}

ネットワーク・モニターで [Enterprise Plan ネットワークの名前を変更](#ep-network-name)できます。

ネットワーク・モニターの 3 つのセクションには、以下の画面が表示されます。 ネットワーク・モニターの左側のナビゲーターから各画面にナビゲートできます。
- **「マイ・ネットワーク」**セクションには、「[概説](#overview)」、「[メンバー](#members)」、「[チャネル](#channels)」、「[通知](#notifications)」、「[API](#apis)」の各画面が表示されます。
- **「マイ・コード (My code)」**セクションには、「[コードの開発 (Develop code)](#write_code)」、「[コードのインストール (Install code)](#chaincode)」、「[サンプルの試行 (Try samples)](#samples)」の各画面が表示されます。
- 「[ヘルプの利用](#support)」画面には、Helios と Hyperledger Fabric ({{site.data.keyword.blockchainfull_notm}} Platform の基礎となっているコード・ベース) のサポート情報とリリース・ノートが表示されます。

ネットワーク・モニターの右上にあるドロップダウン・メニューから、[ネットワーク設定の確認と構成](#network-preferences)を行えます。

このチュートリアルでは、上記の各画面および機能について説明します。

## ネットワーク名の更新
{: #ep-network-name}

Enterprise Plan ネットワークを作成すると、{{site.data.keyword.blockchainfull_notm}} Platform がそのネットワークに名前を割り当てます。ただし、このネットワーク名はネットワーク・モニターでいつでも更新できます。

ネットワーク・モニターの左側にあるナビゲーターの上部でネットワーク名をクリックすると、フィールドが編集可能になります。使用する新規ネットワーク名を入力し、**Enter** キーを押します。ネットワーク名は数秒で更新されます。

**図 1** に、スターター・プランのネットワーク名を、割り当てられた名前から「Starter Plan Network」に更新する手順を示します。

![ネットワーク名の更新](images/update_network_name_ep.gif "ネットワーク名の更新")
*図 1. ネットワーク名の更新*


## 概要
{: #overview}

「概要」画面には、順序付けサービス、CA、ピア・ノードなどのブロックチェーン・リソースについてのリアルタイムの状況情報が表示されます。 **「タイプ」**、**「名前」**、**「状況」**、**「アクション」** という 4 つの別々のヘッダーの下に各リソースが表示されます。 ブロックチェーン・ネットワークの作成中に、順序付けサービス・ノード 3 つと CA ノード 2 つが自動的に作成されます。 CA ノードはメンバーに固有のノードですが、順序付けサービス・ノードはネットワーク全体で共有される共通のエンドポイントです。

**図 2** に「概要」画面を示します。

![「概要」画面](images/myresources.png "ネットワークの概要")
*図 2. ネットワークの概要*

### ノード・アクション
表の**「アクション」**ヘッダーには、リソースを開始または停止するためのボタンがあります。 複数のノードを選択し、**「選択済みを開始 (Start Selected)」**ボタンまたは**「選択済みを停止 (Stop Selected)」**ボタンをクリックして、ノードのグループを開始または停止することもできます。 **「選択済みを開始 (Start Selected)」**ボタンまたは**「選択済みを停止 (Stop Selected)」**ボタンは、1 つまたは複数のノードを選択すると、表の上部に表示されます。

順序付けサービス・ノードでは停止アクションと開始アクションは使用できないことに注意してください。 一般に、ネットワーク上のピア・ノードまたは CA ノードを停止したり開始したりする必要はありません。 停止アクションと開始アクションは、例えばクリーンな状態にするためにピアを再始動する必要がある場合に備えて用意されています。

**「アクション」**ヘッダーの下のドロップダウン・リストから**「ログの表示 (View Logs)」**をクリックして、コンポーネントのログを確認することもできます。 ログでは、さまざまなネットワーク・リソース間で出された呼び出しを調べることができるため、デバッグやトラブルシューティングに役立ちます。 例えば、ピアを停止してトランザクションでそれをターゲットにしようとすると、接続エラーが発生します。 ピアを再始動してトランザクションを再試行すると、接続が成功します。 チャネルがトランザクション処理を続行しているときに、長期間にわたってピアをダウン状態のままにすることもできます。 ピアが再び稼働すると、台帳が同期されていることが分かります。これは、ピアがダウン状態の間にコミットされたブロックを受信するためです。 台帳が完全に同期されたら、通常の呼び出しとそれに対する照会を実行できます。

### 接続プロファイル
{: #enterprise-connection-profile}
**「接続プロファイル」 **ボタンをクリックすると、各リソースの低レベル・ネットワーク情報についての JSONファイルが表示されます。 接続プロファイルには、アプリケーションに必要なすべての構成情報が含まれています。 ただし、このファイルには特定のコンポーネントと順序付けプログラムのアドレスのみが含まれているため、追加のピアをターゲットにする必要がある場合は、それらのエンドポイントを取得する必要があります。 「url」を含むヘッダーに、各コンポーネントの API エンドポイントが表示されます。 クライアント・サイド・アプリケーションから特定のネットワーク・コンポーネントをターゲットにするためには、これらのエンドポイントが必要です。また、エンドポイントの定義は一般にはアプリに付随する JSON モデルの構成ファイルに存在します。 組織外のピアからの承認を必要とするアプリケーションをカスタマイズする場合は、担当のオペレーターからアウト・オブ・バンド操作でそのピアの IP アドレスを取得する必要があります。 クライアントは、応答を返してもらう必要のあるすべてのピアに接続できなければなりません。

### ピアの追加
{: #peers}
**「ピアの追加」**ボタンをクリックして、ネットワークにピア・ノードを追加できます。 Starter Plan では、ネットワーク作成時に 2 つのピアが自動的に追加されます。 Enterprise Plan では、初めてネットワークを作成するときやネットワークに参加するとき、あるいは後でネットワーク・モニターで、ピア・ノードを追加できます。 追加のピアが必要なさまざまなシナリオが考えられます。  例えば、冗長性のために複数のピアが同じチャネルに参加するようにすることができます。 各ピアはチャネルのトランザクションを処理し、台帳のそれぞれのコピーに書き込みます。 いずれかのピアが失敗した場合でも、他のピアはトランザクションとアプリケーション要求の処理を続行できます。  すべてのアプリケーション要求をピア間で対称的にロード・バランシングすることも、機能ごとに異なるピアをターゲットにすることもできます。 例えば、あるピアを台帳の照会用に使用し、別のピアを台帳更新のエンドースメント処理用に使用することができます。

  「ピアの追加 (Add Peers)」ポップアップ・パネルで、追加するピア・ノードの数を選択します。 <!--Currently only "small" peers are available for purchase, however there will eventually be "medium" and "large" to help accommodate larger workloads and higher transaction throughput.-->

## メンバー
{: #members}
「メンバー」画面には、ネットワーク・メンバー情報を表示する「メンバー」タブと、証明書情報を表示する「証明書」タブという 2 つのタブがあります。

### メンバー
{: #members_tab}
**図 3** に、ネットワーク・メンバーが「メンバー」タブに表示されている「メンバー」画面の初期画面を示します。

![「メンバー」画面の「メンバー」タブ](images/monitor_members.png "ネットワーク・メンバー")
*図 3. ネットワーク・メンバー*

ネットワークを作成したときに招待したメンバーに加えて、「メンバー」タブから他のメンバーを招待することができます。 ネットワークにメンバーを招待するには、機関名とオペレーターの E メール・アドレスを入力して**「メンバーの追加」**をクリックします。 ネットワークには、最大で 15 のメンバーが参加できます (ネットワークのイニシエーターを含む)。 ネットワークからメンバーを削除するには、メンバーの行の最後にある「削除」記号をクリックします。

### 証明書
**図 4** に、メンバーの証明書が「証明書」タブに表示されている「メンバー」画面の初期画面を示します。

![「メンバー」画面の「証明書」タブ](images/monitor_certificates.png "証明書")
*図 4. 証明書*

オペレーターは、同じ機関に属するメンバーの証明書を「証明書」タブで管理できます。 **「証明書の追加」**をクリックして、「証明書の追加」パネルを開きます。 証明書に名前を指定し、「鍵」フィールドにクライアント・サイドの PEM 形式の証明書を貼り付け、**「実行依頼 (Submit)」**をクリックします。 このクライアント・サイドの証明書を有効にするためにピアを再始動する必要があります。

証明書の鍵の生成について詳しくは、[クライアント・サイドの証明書の生成](v10_application.html#generating-the-client-side-certificates)を参照してください。

## チャネル
{: #channels}

ネットワークをチャネルに分割できます。各チャネルは、そのチャネルでインスタンス化されたチェーンコードのデータを表示することを許可されたメンバーのサブセットを表します。 トランザクションを実行するためには、すべてのネットワークに 1 つ以上のチャネルが必要です。 チャネルごとに固有の台帳があり、その台帳に対して読み取り/書き込み操作を実行するには、ユーザーは正しく認証される必要があります。 チャネルに参加していないユーザーは、データを表示できません。

**図 5** に、ネットワークのすべてのチャネルの概要を表示するダッシュボードの初期画面を示します。

![チャネル](images/channels.png "チャネル")
*図 5. チャネル*

チャネルを作成すると、チャネル固有の台帳が生成されます。 詳しくは、[チャネルの作成](howto/create_channel.html)を参照してください。

また、既存のチャネルを選択して、チャネル、メンバーシップ、アクティブ・チェーンコードに関する詳細を表示することもできます。 詳しくは、[ネットワークのモニター](howto/monitor_network.html)を参照してください。

## 通知
{: #notifications}

「通知」画面では、保留中の要求を処理したり、完了した要求を表示したりできます。

**図 6** に「通知」画面を示します。

![通知](images/notifications.png "通知")
*図 6. 通知*

チャネルを作成した場合、または新規チャネルに招待された場合、ネットワーク・モニターに通知が表示されます。

要求は「すべて」、「保留中」、「完了」の各サブタブにグループ分けされています。 各サブタブに含まれている要求の数が、サブタブのヘッダーの後ろに表示されています。
   * 「すべて」サブタブには、すべての要求が含まれています。
   * 承認も拒否もしていない要求、まだ参照していない要求は、「処理待ち (Pending)」サブタブに含まれています。 **「要求の確認 (Review Request)」**ボタンをクリックし、チャネル・ポリシーやメンバーなども含めて要求と投票状況を確認します。 チャネル・オペレーターは、要求の**受諾**または**拒否**を行なったり、**「後で」**をクリックしてそれを別の時に処理したりできます。 要求が十分な数のチャネル・オペレーターから承認された場合は、**「要求の実行依頼 (Submit Request)」**をクリックしてチャネルの更新をアクティブ化します。
   * 実行依頼した要求は「完了」サブタブに表示されます。  **「要求の確認 (Review Request)」**をクリックして、その詳細を確認できます。

要求のリストが長い場合は、上部の検索フィールドで要求を検索できます。

保留中の要求は、要求の前のチェック・ボックスを選択し、**「要求の削除 (Delete Request)」**をクリックして削除できます。 完了した要求は削除できません。

## API
{: #apis}

アプリケーション開発を容易にするために、{{site.data.keyword.blockchainfull_notm}} Platform は、Swagger UI でネットワークに対してテストできる API を公開しています。

**図 7** に「API」画面を示します。

![API](images/API_screen.png "API")
*図 7. API*

**「Swagger UI」**リンクをクリックして Swagger UI を開きます。 API を実行するには、その前にネットワーク資格情報 (この API ページにあります) を使用して Swagger UI に権限を与える必要があることに注意してください。 詳しくは、[Swagger API を使用したネットワークとの対話](howto/swagger_apis.html)を参照してください。

## コードの開発 (Develop Code)
{: #write-code}

Enterprise Plan は {{site.data.keyword.blockchainfull_notm}} Platform: Develop を統合し、業界標準のツールとテクノロジーを備えた開発環境を提供します。 オンラインまたはローカルのいずれの環境でもネットワークを開発できます。 ネットワークを開発したら、Enterprise Plan ネットワークに再びデプロイすることができます。

**図 8** は、「コードの開発 (Develop code)」画面を示しています。

![コードの開発 (Develop code)](images/write_code.png "コードの開発 (Develop code)")
*図 8. コードの開発 (Develop code)*

Enterprise Plan でコードを開発してデプロイする方法について詳しくは、[Enterprise Plan でのビジネス・ネットワークの開発](develop_enterprise.html)を参照してください。

## コードのインストール (Install code)
{: #chaincode}

チェーンコードは、「スマート・コントラクト」とも呼ばれるソフトウェアの一部分で、そこには台帳を照会および更新するための機能一式が含まれています。 これらはピアにインストールされ、チャネル上でインスタンス化されます。

**図 9** に「コードのインストール」画面を示します。

![コードのインストール (Install code)](images/chaincode_install_overview.png "コードのインストール (Install code)")
*図 9. コードのインストール (Install code)*

チェーンコードは、まずピアのファイル・システムにインストールされてから、チャネルでインスタンス化されます。 詳しくは、[チェーンコードのインストール、インスタンス化、および更新](howto/install_instantiate_chaincode.html)を参照してください。

## サンプルの試行
{: #samples}

サンプル・アプリケーションは、ブロックチェーン・ネットワークとアプリケーション開発についての理解を深めるのに役立ちます。 Marbles サンプル・アプリケーションをインストールする方法については、ネットワーク・モニターで Marbles リポジトリーへのリンクをたどってください。 独自のサンプルを開発してデプロイする方法について詳しくは、[アプリケーションの開発](v10_application.html)を確認してください。

**図 10** に「サンプルの試行」画面を示します。

![サンプルの試行](images/sample_overview_ep.png "サンプルの試行")
*図 10. 「サンプル」*

## ヘルプの利用
{: #support}

「ヘルプの利用」画面には 2 つのタブがあります。「サポート」タブではサポート情報を提供し、「リリース・ノート」タブでは各リリースの新機能や変更された機能を記載しています。

**図 11** に、サポート情報が「サポート」タブに表示されている「サポート」画面の初期画面を示します。

![サポート](images/support.png "サポート")
*図 11. ブロックチェーン・サポート*

このページのリンクおよびリソースを使用して、トラブルシューティング・フォーラムおよびサポート・フォーラムにアクセスします。

* [{{site.data.keyword.blockchainfull_notm}} サービス資料](index.html)の**概説** (この資料サイト) には、{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.blockchainfull}} Platform を初めて使用する場合のガイドが用意されています。 左側のナビゲーターから対応するトピックを見つけるか、上部の検索機能を使用して用語を検索できます。
* [IBM Developer Works ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://developer.ibm.com/blockchain/) の**コミュニティーのヘルプ**には、開発者向けのリソースや情報があります。
* **サポート・チケット**の下の [IBM dWAnswers ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://developer.ibm.com/answers/smartspace/blockchain/) は、質問と回答のやり取りを行うプラットフォームの役割を果たします。 過去に投稿された質問から回答を探したり、新しい質問を送信したりできます。 質問にはキーワード **blockchain** を含めてください。
  また、**「{{site.data.keyword.Bluemix_notm}} サポート・チケットのオープン」** オプションを使用して、チケットを {{site.data.keyword.blockchainfull_notm}} サポート・チームに送信することもできます。  該当する特定の {{site.data.keyword.Bluemix_notm}} インスタンスの詳細およびコード・スニペットを提供してください。
* [サンプル・アプリケーション ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://github.com/ibm-blockchain) の**ブロックチェーン・サンプル・アプリケーション**には、アプリケーションの開発を支援するガイドやサンプル・コード・スニペットが用意されています。
* [Hyperledger Fabric ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](http://hyperledger-fabric.readthedocs.io/) と [Hyperledger Fabric コミュニティー ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](http://jira.hyperledger.org/secure/Dashboard.jspa) の **Hyperledger Fabric** には、Hyperledger Fabric スタックに関する詳細を調べることができます。
  [Hyperledger Expert ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://chat.hyperledger.org/channel/general) では、Hyperledger Fabric コードについて質問することができます。

問題をデバッグできない場合や、疑問点の答を突き止めることができない場合は、IBM Cloud サービス・ポータルでサポート・ケースを送信してください。 詳しくは、[サポートのページ](ibmblockchain_support.html)を参照してください。

図 12 と図 13 は、「リリース・ノート」タブに各リリースの新機能と変更機能が表示される「ヘルプの利用」の初期画面を示しています。

![リリース・ノート Helios](images/releasenotes_helios.png "リリース・ノート Helios")
*図 12. Helios のリリース・ノート*

![リリース・ノート Fabric](images/releasenotes_Fabric.png "リリース・ノート Fabric")
*図 13. Fabric のリリース・ノート*


## ネットワーク設定 (Network preferences)
{: #network-preferences}

右上隅をクリックし、ドロップダウン・メニューを開いて、**「ネットワーク設定 (Network preferences)」**を開きます。「ネットワーク設定 (Network preferences)」ウィンドウが開きます。「ネットワーク設定 (Network preferences)」ウィンドウには、ネットワーク名、Fabric のバージョン、{{site.data.keyword.cloud_notm}} 内のネットワーク・ロケーション、台帳データベース・タイプなど、ネットワークの基本情報が表示されます。

Enterprise Plan ネットワークは近々 Fabric v1.1 にアップグレードされます。<!-- May 15th, 2018 will run on Hyperledger Fabric v1.1-->アップグレード後にネットワークを作成した場合は、「ネットワーク設定 (Network preferences)」ウィンドウでネットワークの Web 非アクティブ・タイムアウトと相互 TLS も管理することができます。これらの設定を変更できるのは、ネットワーク・イニシエーターのみです。

<!--
Enterprise Plan networks that are created after May 15th, 2018 will run on Hyperledger Fabric v1.1. If you create networks after the upgrade, you can also manage web inactivity timeout, mutual TLS, and switch your ledger to CouchDB for your network in the Network preferences window. These settings can be changed by the network initiator only.
-->

### Web 非アクティブ・タイムアウト (Web inactivity timeout)
{: #web-inactivity-timeout}

**注**: Web 非アクティブ・タイムアウト設定を変更できるのは、**ネットワーク・イニシエーター**のみです。これはネットワーク・レベルの設定であり、すべてのネットワーク・メンバーに影響します。

デフォルトでは、Web 非アクティブ・タイムアウトは**「オフ」**に設定されます。Web 非アクティブ・タイムアウトを**オン**にした場合、非アクティブ状態が 10 分続いたネットワーク・メンバーはすべて自動的にログアウトされます。Web 非アクティブ・タイマーが 10 分に達すると、ネットワーク・メンバーのアカウントのセキュリティーを確保するために、Web 非アクティブ・タイムアウト機能によって非アクティブな Web セッションが終了させられます。リンクをクリックするか、ネットワーク・モニターを更新すると、Web 非アクティブ・タイマーはリセットされます。10 分に達する前にブラウザーのウィンドウまたはタブを閉じた場合も、Web セッションは終了します。

### 相互 TLS (Mutual TLS)
{: #mutual-tls}

相互 TLS により、アプリケーションとネットワークの間の通信を保護し、ネットワークと通信できるユーザーを限定できます。

**注**: 相互 TLS を有効または無効にできるのは、**ネットワーク・イニシエーター**のみです。これはネットワーク・レベルの設定であり、すべてのネットワーク・メンバーに影響します。

デフォルトでは、「相互 TLS (mutual TLS)」ボタンは**「オフ」**に設定されています。相互 TLS を有効にする場合は、この機能をサポートするようにアプリケーションを更新する必要があります。そうしないと、アプリケーションはネットワークと通信できません。

Fabric 1.1 Enterprise Plan ネットワークの場合は、組織ごとに独自の相互 TLS 認証局 (CA) が使用されます。相互 TLS の CA に接続するために必要な情報は、ネットワーク・モニターの**「概要」**画面で**「接続プロファイル (Connection Profile)」**ボタンをクリックしてアクセスできる[接続プロファイル](##enterprise-connection-profile)で確認できます。接続プロファイルには、CA に接続し、ネットワークに接続するために必要な証明書を取得するための必須情報が含まれています。

接続プロファイルで `certificateAuthorities` セクションを見つけます。このセクションには、相互 TLS を使用してネットワークと通信するための証明書を登録および取得するために必要な以下の属性があります。

- `url`: 相互 TLS 証明書を提供できる CA に接続するための URL
- `enrollId`: 証明書を取得するために使用する登録 ID
- `enrollSecret`: 証明書を取得するために使用する登録シークレット
- `x-tlsCAName`: アプリケーションが相互 TLS を使用して通信できるようにする証明書を取得するために使用する CA 名。

相互 TLS をサポートするようにアプリケーションを更新する方法について詳しくは、[How to configure mutual TLS ![外部リンク・アイコン](images/external_link.svg "外部リンク・アイコン")](https://fabric-sdk-node.github.io/tutorial-mutual-tls.html) を参照してください。

<!--
### CouchDB ledger type
{: #couchdb}
**Note**: Only the **network initiator** can switch the ledger database from LevelDB to CouchDB. This is a network level setting and will affect all network members. Switching to CouchDB is permanent. You cannot revert back to LevelDB.
Before Enterprise Plan upgrades to Fabric v1.1, all network peers store data in the pure key-value LevelDB. With Fabric v1.1, you can choose to use CouchDB as your ledger database. CouchDB is a document datastore that permits indexing the contents of your data and allows you to issue rich queries against the data on your peer. Note that Hyperledger Fabric does not support peers running different databases. If CouchDB is used, it must be used by all of the peers.
To use CouchDB, your data must be stored in a data format that can be modeled in chaincode, such as JSON. If the decision is made to migrate from LevelDB to CouchDB, the {{site.data.keyword.blockchainfull_notm}} Platform will migrate your data from key-value format to the CouchDB format automatically.
If you switch to CouchDB, you need to update your chaincode to take advantage of indexes and rich queries. For more information about CouchDB and how to set up index, see [CouchDB as the State Database ![External link icon](images/external_link.svg "External link icon")](https://hyperledger-fabric.readthedocs.io/en/latest/couchdb_as_state_database.html). For more information about updating chaincode in {{site.data.keyword.blockchainfull_notm}} Platform, see [Updating a chaincode](howto/install_instantiate_chaincode.html#updating-a-chaincode).
-->

次の**図 14** は、「ネットワーク設定 (Network preferences)」ウィンドウを示しています。

<!-- ![Network preferences](images/network_preferences_ep.gif "Network preferences") -->
![ネットワーク設定 (Network preferences)](images/network_preferences_ep_tmp.png "ネットワーク設定 (Network preferences)")  
*図 14. ネットワーク設定 (Network preferences)*
