---

copyright:
  years: 2019
lastupdated: "2019-04-03"

subcollection: blockchain

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 組織の管理
{: #ibp-console-organizations}

{{site.data.keyword.blockchainfull}} Platform コンソールを使用して、メンバーシップ・サービス・プロバイダー (MSP) と呼ばれる正式な組織定義を作成できます。 組織の MSP 定義を作成すれば、ブロックチェーン・コンソーシアムの他のメンバーが、この組織のノードやアプリケーションのアイデンティティーを確認できるようになります。 MSP 定義には組織の管理者の証明書も含まれています。

コンソールを使用して、ネットワークのメンバーとして参加する組織を管理することもできます。 順序付けサービスの管理者は、組織タブを使用してブロックチェーン・[コンソーシアム](/docs/services/blockchain/glossary.html#glossary-consortium)にメンバーを追加できます。 その後は、コンソーシアムのメンバーが、コンソールを使用して新規チャネルまたは既存のチャネルにメンバーを追加できます。

**対象者:** このトピックは、ブロックチェーン・ネットワークの作成、モニター、管理を担当するネットワーク・オペレーターを対象に設計されています。

## MSP について
{: #console-organizations-about-msp}

Hyperledger Fabric をベースとする {{site.data.keyword.blockchainfull_notm}} Platform は、許可制ブロックチェーン・ネットワークを構築します。 参加者がトランザクションを送信し、台帳上の資産と対話するには、その参加者がネットワークに認識されている必要があります。 Fabric では、コンソーシアムと呼ばれる、招待された組織のグループを介してアイデンティティーを認識します。 コンソーシアムの各組織は、有効な資格情報をメンバーに発行し、そのメンバーがネットワークの参加者になれるようにすることができます。 その後、参加者はブロックチェーン・ノードを操作し、クライアント・アプリケーションからトランザクションを送信できます。

コンソーシアムの各組織は、ルート CA と呼ばれる独自の認証局を運用する必要があります。 この認証局 (またはその中間 CA) が、組織に属するすべての ID を作成し、各 ID に公開鍵と秘密鍵を発行します。 それらの鍵には CA の署名が付いており、組織のメンバーは、これらを使用してアクションの署名付けと検証を行います。 コンソーシアムに参加した組織は、他の組織の CA の署名を認識し、その組織のピアやアプリケーションが有効な参加者であることを検証できます。 Hyperledger Fabric のメンバーシップについて詳しくは、Fabric 資料の[メンバーシップの概念についてのトピック ![外部リンク・アイコン](../images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/membership/membership.html "Membership") を参照してください。

コンソーシアムに参加する組織は、**メンバーシップ・サービス・プロバイダー (MSP)** と呼ばれる組織定義を作成しておく必要があります。 この MSP には以下の情報が含まれています。
- **ルート認証局**によって署名された証明書。 この証明書は、ノード、チャネル、およびアプリケーションのアイデンティティーを検証するために使用されます。
- **TLS CA** によって署名された証明書。 ルート TLS 証明書を使用することにより、ピアは組織間のゴシップに参加できます。このゴシップは、Hyperledger Fabric の[**プライベート・データ**・コレクション](/docs/services/blockchain/howto/ibp-console-smart-contracts.html#ibp-console-smart-contracts-private-data)および[サービス・ディスカバリー ![外部リンク・アイコン](../images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html "Service discovery") の機能を利用するために必要です。
- **MSP ID**。 MSP ID は、コンソーシアム内の組織の正式名です。 ノードとアプリケーションの MSP ID を覚えておく必要があります。
- **ピア管理者** ID および**組織管理者** ID の**管理者証明書**。 これらの証明書は、順序付けサービスに渡されて、チャネルの作成または編集を許可されている組織内の ID を確認するために使用されます。 コンソールを使用して順序付けプログラムまたはピアを作成すると、MSP 内の管理者証明書がそれらの新しいノードにデプロイされます。 そして、コンソールまたはクライアント・アプリケーションから、それらの証明書を使用することで、そのピアまたは順序付けプログラムを操作することができます。

## コンソールでの MSP の管理

**「組織」**タブにナビゲートします。 このタブで、コンソールに存在する認証局を使用して、[MSP 定義を作成](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-create-msp)できます。 また、このタブでは、別の組織で作成された [MSP をインポート](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-import-msp)することもできます。

作成またはインポートしたすべての MSP を**「使用可能な組織 (Available Organizations)」**で参照できます。 この「組織」タブの MSP 定義を使用することで、次の重要な機能をコンソールで実行できます。
- ピアまたは順序付けプログラムのノードを作成する場合は、その新しいノードに管理者証明書を提供するために組織の MSP が使用されます。
- 順序付けノードの管理者は、MSP を使用して、[新しい組織をコンソーシアムに追加](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-add-consortium)できます。
- コンソーシアムのメンバーは、他のコンソーシアム・メンバーの MSP をコンソールにインポートして、そのメンバーを新規または既存のチャネルに追加できます。

## 組織の MSP の作成
{: #console-organizations-create-msp}

**「組織」**タブを使用して、組織の MSP 定義を生成できます。 **「MSP の作成 (Create MSP)」**をクリックすると、サイド・パネルが開き、必要なすべての情報 (ルート CA、MSP ID、および組織の管理者) を入力できます。

- パネルの**「MSP 詳細 (MSP details)」**セクションを使用して、組織の MSP ID を選択します。 この ID は、ネットワークの他のメンバーがこの組織を参照する際に使用する正式名です。 **MSP ID を保存します。**

- **「ルート認証局の詳細 (Root Certificate Authority details)」**セクションを使用して、組織のルート CA を選択します。 これは、組織に属するすべてのノード ID とアプリケーション ID の作成に使用した (または今後使用する) CA です。 中間 CA を使用する場合は、それらの中間 CA を作成するために使用した CA です。 コンソールで管理している CA のリストからルート CA を選択します。 コンソールを使用して CA を作成した場合、ルート CA として選択すると、ルート TLS 証明書も作成されます。

- この**「ルート認証局の詳細 (Root Certificate Authority details)」**セクションを使用して、組織管理者の証明書を生成することもできます。 組織の MSP 定義を作成する前に、組織管理者とノード管理者をルート CA に登録しておく必要があります。 そして、それらの ID を使用してネットワークを操作するために、以下の手順を実行する必要があります。

  1. 管理者 ID ごとに公開鍵と秘密鍵のペアを作成します。
  2. 各管理者 ID の公開鍵 (証明書) を MSP 定義に指定します。
  3. ID をコンソール・ウォレットに追加します。 コンソールを使用して作成されたノードまたはチャネルは、MSP からの証明書を使用して、どのユーザーが有効な管理者であるかをチェックします。 そのため、管理者証明書を MSP に追加するときに使用したものと同じ公開鍵と秘密鍵のペアを、コンソール・ウォレット内に保管する必要があります。

  **「MSP 定義の作成 (Create MSP definition)」**パネルを使用して、管理者 ID に対してこれらの操作を実行できます。 ルート CA を選択したら、**「組織管理者証明書の生成 (Generate organization admin certificate)」**セクションで以下の手順を実行します。
  1. ルート CA に登録した管理者 ID の登録 ID と登録シークレットを入力します。 登録 ID と登録シークレットを入力したら、コンソール・ウォレットに ID を表示するときの名前を選択します。
  2. **「生成」**をクリックします。 これにより、公開鍵と秘密鍵の新しいセットが生成され、それらの鍵がコンソール・ウォレットに自動的に追加されます。 ウォレットでは、管理者 ID はこのパネルで選択した名前で表示されます。 これらの鍵は、ブラウザーのローカル・ストレージにしか保管されないので、ブラウザーを変更すると、コンソール・ウォレットに表示されなくなります。 元のブラウザーから ID をエクスポートし、新しいブラウザーのコンソール・ウォレットにインポートする必要があります。
  3. 次に、**「エクスポート」**をクリックしてファイル・システムに鍵ペアをダウンロードし、安全な場所に保管します。

- サイド・パネルの**「管理者 (オプション) (Administrators (Optional))」**セクションに管理者の公開鍵が含まれています。 **「組織管理者証明書の生成 (Generate organization admin certificate)」**セクションを使用して生成した証明書は、**「管理者証明書 (admin certificate)」**フィールドの最初の行にあります。複数の管理者 ID を使用してネットワークを操作する場合、追加のノード管理者または組織管理者の証明書を**「管理者証明書 (admin certificate)」**フィールドに貼り付けることができます。

管理者証明書は MSP 定義を使用してノードおよびチャネルに渡されるので、ノード管理者と組織管理者の各証明書が MSP に保管されていることを確認する必要があります。 コンソールを使用して順序付けプログラム、ピア、またはチャネルを作成するときに、コンソール・ウォレットにエクスポートしたいずれかの ID を、MSP 定義に指定されている管理者証明書に**関連付ける**必要があります。 **「ID の関連付け (Associate identity)」**セクションまたはパネルが表示されたら、MSP 定義の作成時に生成してウォレットに保存した ID を選択します。

ルート CA、MSP ID、および作成した管理者証明書を選択したら、**「MSP 定義の作成 (Create MSP definition)」**をクリックして、MSP 定義を作成します。 定義が、「組織」タブに組織としてリストされるようになります。 ノードをデプロイして、ブロックチェーン・コンソーシアムに参加するときには、この MSP 定義を使用することになります。

## MSP の JSON ファイルの手動作成
{: #console-organizations-build-msp}

**これは、ブロックチェーンの ID 管理における証明書の使用方法に詳しい上級者ユーザー向けのオプションです。**

**外部 CA** ({{site.data.keyword.IBM_notm}} がホストする CA ではないもの) で作成された証明書をピアまたは順序付けプログラムに使用する場合は、ピア組織または順序付けプログラム組織の MSP 定義を表す MSP 定義 JSON ファイルを作成する必要があります。以下の形式を使用して JSON ファイルを作成します。

```
{
    "name": "<organization_name>",
    "msp_id": "<organization_id>",
    "type": "msp",
    "root_certs": [
        "<root_certs>"
    ],
     "intermediate_certs": [
         "<intermediate_certs>"
     ],
    "admins": [
        "<admins>"
    ],
    "tls_root_certs": [
        "<tls_root_certs>"
    ],
    "tls_intermediate_certs": [
        "<tls_intermediate_certs>"
    ]
}
```
{:codeblock}

- **organization_name**: コンソールでこの MSP 定義を識別するために使用する名前を指定します。
- **organization_id**: コンソールでこの MSP を内部的に表すために使用する ID を指定します。
- **root_certs**: (オプション) 外部 CA で作成された `base64` 形式のルート証明書を 1 つ以上含む配列を貼り付けます。CA ルート証明書または中間 CA 証明書のどちらかを指定する必要があります。両方を指定することもできます。
- **intermediate_certs**: (オプション) 外部の中間 CA で作成された `base64` 形式の証明書を 1 つ以上含む配列を貼り付けます。CA ルート証明書または中間 CA 証明書のどちらかを指定する必要があります。両方を指定することもできます。
- **admins**: 組織管理者の `base64` 形式の署名付き証明書を貼り付けます。
- **tls_root_certs**: (オプション) TLS CA で作成された `base64` 形式のルート証明書を 1 つ以上含む配列を貼り付けます。外部 TLS CA のルート証明書または外部中間 TLS の CA 証明書のどちらかを指定する必要があります。両方を指定することもできます。
- **tls_intermediate_certs**: (オプション) 中間 TLS CA で作成された `base64` 形式の証明書を 1 つ以上含む配列を貼り付けます。外部 TLS CA のルート証明書または外部中間 TLS の CA 証明書のどちらかを指定する必要があります。両方を指定することもできます。  

MSP 定義では、以下の追加フィールドも使用できますが、必須ではありません。
- **organizational_unit_identifiers**: この MSP の有効なメンバーの各 X.509 証明書に含める必要がある組織単位 (OU) のリスト。これは、複数の組織で同じトラスト・ルートと中間 CA を利用し、組織ごとに自組織メンバーのために OU フィールドを予約している場合に使用するオプションの構成パラメーターです。多くの場合、組織は職務ごとに複数の組織単位 (OU) に分割されます。例えば、ORG1 組織には、製造業務と販売業務という別々の基幹業務を表す ORG1-MANUFACTURING と ORG1-DISTRIBUTION という OU があるかもしれません。CA が発行する X.509 証明書の OU フィールドには、そのアイデンティティーが属する基幹業務が指定されます。詳しくは、Fabric の資料の [Identity Classification ![外部リンク・アイコン](../images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/latest/msp.html#identity-classification "Identity Classification") のトピックを参照してください。  
- **fabric_node_OUs**: アイデンティティー分類を可能にする Fabric 固有の OU。`NodeOUs` には、クライアント、ピア、順序付けプログラムをそれぞれの OU に基づいて区別する方法についての情報が含まれます。Enabled を true に設定してチェックを実施する場合、MSP は、アイデンティティーが `client`、`peer`、または `orderer` のアイデンティティーである場合に、そのアイデンティティーを有効と見なします。アイデンティティーには、このような特別な OU のうちの 1 つだけを指定する必要があります。MSP で `fabric_node_OU` を指定する方法の例については、[Fabric Service Discovery の資料 ![外部リンク・アイコン](../images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric.readthedocs.io/en/latest/discovery-cli.html#configuration-query) のトピックを参照してください。
- **revocation_list**: 有効でなくなった証明書のリスト。X.509 ベースのアイデンティティーの場合、これらのアイデンティティーは、Subject Key Identifier (SKI) および Authority Access Identifier (AKI) と呼ばれるストリングのペアであり、X.509 証明書を使用するときには、必ず、証明書が失効していないかどうかを確認するためにチェックされます。 [証明書失効リスト ![外部リンク・アイコン](../images/external_link.svg "外部リンク・アイコン")](https://hyperledger-fabric-ca.readthedocs.io/en/release-1.4/users-guide.html?highlight=revocation%20list#revoking-a-certificate-or-identity "証明書またはアイデンティティーの失効") について詳しくは、Fabric の資料のトピックを参照してください。

例えば、以下のような JSON ファイルになります。

```
{
    "name": "Org1 MSP",
    "msp_id": "org1msp",
    "type": "msp",
    "root_certs": [
        "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUNGakNDQWIyZ0F3SUJBZ0lVZFhUcWNZVVhRS3U3WHVQWmcxUHBsekpFVFlNd0NnWUlLb1pJemowRUF3SXcKYURFTE1Ba0dBMVVFQmhNQ1ZWTXhGekFWQmdOVkJBZ1REazV2Y25Sb0lFTmhjbTlzYVc1aE1SUXdFZ1lEVlFRSwpFd3RJZVhCbGNteGxaR2RsY2pFUE1BMEdBMVVFQ3hNR1JtRmljbWxqTS0K"
    ],
    "admins": [
        "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tDQpNSUlDWHpDQ0FnYWdBd0lCQWdJVVp6NFdQdWwxRXRVOUNIcTl4NFg0Y2QwakNpNHdDZ1lJS29aSXpqMEVBd0l3DQphREVMTUFrR0ExVUVCaE1DVlZNeEZ6QVZCZ05WQkFnVERrNXZjblJvSUVOaGNtOXNhVzVoTVJRd0VnWURWUVFLDQpFd3RJZVhCbGNteGxaR2RsY2pFUE1BMEdBMVVFQ3hNR1JtRmljbFLS0tLS0NCg=="
    ],
    "tls_root_certs": [
        "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUNHRENDQWI2Z0F3SUJBZ0lVTzVhWU9WbjNwTkRMZGVLTFlIanRIUEtNTnY4d0NnWUlLb1pJemowRUF3SXcKWFRFTE1Ba0dBMVVFQmhNQ1ZWTXhGekFWQmdOVkJBZ1REazV2Y25Sb0lFTmhjbTlzYVc1aE1SUXdFZ1lEVlFRSwpFd3RJZVhCbGNteGxaR2RsY2pFUE1BMEdBMVVFQ3hNR1JtRmljbWxqTVE0d0RBWamd5TURRM01EQmFNRjB4Q3pBSkJnTlZCQVlUQWxWVE1SY3cKRlFZRFZRUUlFdztLS0K"
    ]
}
```
{:codeblock}

証明書はすべて base64 形式でエンコードしたものでなければならないことに注意してください。
{:important}

`PEM` 形式の証明書ファイル `<cert.pem>` の内容を base64 ストリングに変換するには、ローカル・マシンで次のコマンドを実行します。

```
export FLAG=$(if [ "$(uname -s)" == "Linux" ]; then echo "-w 0"; else echo "-b 0"; fi)
cat <cert.pem> | base64 $FLAG
```
{:codeblock}

この定義を `JSON` ファイルとして保存します。  

外部 CA からの証明書を使用してピア・ノードまたは順序付けプログラム・ノードの組織を定義する MSP 定義を構成しました。これで、[外部 CA からの証明書をピアまたは順序付けプログラムに使用する手順](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network-third-party-ca)に戻ることができます。

## MSP のインポート
{: #console-organizations-import-msp}

新しい組織をコンソーシアムに追加できるのは、順序付けプログラム管理者のみです。 順序付けプログラムの管理者が、コンソーシアムに招待されたすべての組織の MSP 定義を集めて、コンソールにインポートする必要があります。 その後、順序付けプログラムの管理者が、順序付けプログラム・ノードを使用して、それらの MSP を順序付けサービスに追加することができます。

管理者が MSP 定義を作成していれば、他の組織は「組織」タブを使用して MSP を JSON 形式でローカルのファイル・システムにダウンロードできます。 そして、その MSP JSON ファイルを帯域外操作で送ってもらいましょう。 **「組織」**タブに移動し、**「MSP 定義のインポート (Import MSP Definition)」**を使用して、その MSP ファイルをコンソールにインポートします。 MSP 定義が**「使用可能な組織 (Available organizations)」**セクションに表示されたら、自分の順序付けプログラム・ノードに移動し、[その組織をコンソーシアムに追加](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-add-consortium)できます。


## コンソーシアムへの組織の追加
{: #console-organizations-add-consortium}

組織のコンソーシアムは、順序付けサービスによってホストされています。

順序付けサービスの管理者は、コンソールを使用して組織をコンソーシアムに追加することができます。 **「ノード」**タブに移動し、順序付けノードをクリックします。 順序付けノード・パネルの**「コンソーシアム・メンバー (Consortium members)」**で、**「組織の追加 (Add organization)」**をクリックします。 [組織タブにインポートした](/docs/services/blockchain/howto/ibp-console-organizations.html#console-organizations-import-msp) MSP 定義のリストから MSP 定義を選択できるサイド・パネルが開きます。 **「JSON のアップロード (Upload JSON)」**オプションを使用して、他の組織で作成された MSP 定義ファイルを直接インポートすることもできます。

## チャネルの作成および編集
{: #console-organizations-create-channel}

組織がコンソーシアムに追加されたら、組織は順序付けサービスを使用して新しいチャネルを作成したり、既存のチャネルに自身を追加したりできます。 チャネルへの参加 (チャネルにピアを参加させる、スマート・コントラクトをインスタンス化する、トランザクションを送信するなど) に必要な情報は、MSP 定義を使用して提供されます。

コンソーシアムに追加された組織は、以下の手順を使用してチャネルを作成できます。

1. コンソーシアムをホストしている順序付けノードを、自分のコンソールにインポートします。 その順序付けノードの管理者になる必要はありませんが、自分のコンソールで順序付けプログラム・ノードの名前とエンドポイント情報を指定する必要があります。
2. **「組織」**タブで、新しいチャネルに追加する組織の MSP をコンソールにインポートします。 組織をチャネルに追加するには、まず、その組織をコンソーシアムに追加する必要があることに**注意してください**。
3. **「チャネル」**タブに移動し、**「チャネルの作成 (Create channel)」**をクリックします。 チャネル名、メンバーシップ、およびチャネル・ポリシーを指定できるサイド・パネルが開きます。 コンソーシアムに追加されている任意の組織を新規チャネルに追加できます。

これらの手順の詳細については、**ネットワーク構築**チュートリアルの[チャネルの作成](/docs/services/blockchain/howto/ibp-console-build-network.html#ibp-console-build-network-create-channel1)を参照してください。

### チャネル定義の MSP の更新
{: #console-organizations-update-channel}

時間が経過すると、チャネルに既に関連付けられている MSP 定義の証明書を更新しなければならなくなることがあります。 そのような状態になった場合は、以下の手順を実行して、そのチャネルに属する組織の MSP 定義を更新します。  

1. コンソールの**「チャネル」**タブにナビゲートします。
2. 更新する組織の MSP が属するチャネルをクリックして開きます。
3. **「チャネルの詳細 (Channel details)」**タブをクリックします。
4. 更新する関連チャネル・メンバーのタイルをクリックします。
5. 更新した MSP 定義をまだコンソールにインポートしていない場合は、ここでファイルをアップロードできます。 **注:** この操作を実行しても、「組織」タブに表示される関連 MSP 定義は更新されません。 コンソールの「組織」タブで MSP 定義を既に更新している場合は、ドロップダウン・リストからその定義を選択できます。
