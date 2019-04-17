---
title: ソフトウェア定義ネットワークの証明書を管理します。
description: このトピックを使用すると、ソフトウェアによるネットワーク制御 (SDN) で Windows Server 2016 Datacenter を展開するときに、ネットワーク コントローラーの Northbound と Southbound 通信証明書を管理するのに方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3036de9161cabc2f3a85a1d3b2ce7739f0ff6bd3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="manage-certificates-for-software-defined-networking"></a>ソフトウェア定義ネットワークの証明書を管理します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Windows Server 2016 Datacenter にソフトウェアがネットワーク定義 \(SDN\) を展開して、SDN 管理クライアントとして System Center Virtual Machine Manager \(SCVMM\) を使用しているときに、ネットワーク コントローラーの Northbound と Southbound 通信証明書を管理するのに方法について説明します。

>[!NOTE]
>ネットワーク コントローラーの概要については、次を参照してください。[ネットワーク コントローラー](../technologies/network-controller/Network-Controller.md)します。

ネットワーク コントローラーが通信を保護する Kerberos を使用していない場合は、認証、承認、および暗号化の X.509 証明書を使用できます。

SDN Windows Server 2016 Datacenter では、自己署名の両方をサポートし、証明機関 \ (CA\)-X.509 証明書に署名します。 このトピックは、ソフトウェア ロード バランサー \(SLB\) などのネットワーク デバイスと管理のクライアントとネットワーク コントローラーの Northbound の通信チャネルをセキュリティで保護するため、これらの証明書を作成し、適用する方法を手順に沿ってと Southbound の通信を提供します。
.
Certificate\ ベースの認証を使用しているときに、次の方法で使用されているネットワーク コントローラーのノードの 1 つ証明書を登録する必要があります。

1. ネットワーク コントローラーのノードとクライアントの管理、System Center Virtual Machine Manager などの間で Secure Sockets Layer \(SSL\) で Northbound 通信を暗号化します。
2. ネットワーク コントローラーのノードと Southbound のデバイスと、Hyper-V ホストとソフトウェア ロード バランサー \(SLBs\) などのサービスの間で認証されます。

## <a name="creating-and-enrolling-an-x509-certificate"></a>作成して、X.509 証明書の登録

作成し、CA によって発行された証明書または自己署名証明書のいずれかを登録できます。

>[!NOTE]
>SCVMM を使用して、ネットワーク コントローラーを展開する場合は、通信を暗号化する Northbound ネットワーク コントローラーのサービス テンプレートの構成中に使用される X.509 証明書を指定する必要があります。

証明書の構成は、次の値を含める必要があります。

- 値、**RestEndPoint**かに、テキスト ボックスに、ネットワーク コントローラー完全修飾ドメイン名 \(FQDN\) または IP アドレスをする必要があります。 
- **RestEndPoint**値は、サブジェクト名と一致する必要があります \ (共通名、CN\) の X.509 証明書。

### <a name="creating-a-self-signed-x509-certificate"></a>自己署名の X.509 証明書の作成

自己署名入りの X.509 証明書を作成し、秘密キーと共にエクスポートすることができます \ (、password\ で保護されている)、次のネットワーク コントローラーのシングル ノードおよび複数ノードの展開の手順です。

自己署名証明書を作成するときに、次のガイドラインを使用することができます。

- DnsName パラメーター - ネットワーク コントローラーの REST エンドポイントの IP アドレスを使用することができますが、これは推奨されません、ネットワーク コントローラーのノードがすべて、1 つの管理サブネット内にあることが必要な \ (例: [1 つの rack\)
- 複数の NC ノード展開の DNS 名を指定することになる、ネットワーク コントローラーのクラスターの FQDN \ (DNS ホスト A レコードが自動的に作成されます \)。 
- 1 つのノードのネットワーク コントローラーの展開では、ネットワーク コントローラーのホスト名の後ろに完全なドメイン名が DNS 名にできます。

#### <a name="multiple-node"></a>複数のノード

使用することができます、[New-selfsignedcertificate](https://technet.microsoft.com/en-us/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)自己署名証明書を作成する Windows PowerShell コマンド。

**構文**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**使用例**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>1 つのノード

使用することができます、[New-selfsignedcertificate](https://technet.microsoft.com/en-us/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)自己署名証明書を作成する Windows PowerShell コマンド。

**構文**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**使用例**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>CA\ で署名された X.509 証明書の作成

CA を使用して、証明書を作成するにする必要がありますが既に展開されている Active Directory Certificate Services \(AD CS\) と公開キー基盤 \(PKI\) します。 

>[!NOTE]
>ただし、このトピックの手順には、AD CS に固有のネットワーク コントローラーと用の証明書を作成するのには、サード パーティの Ca または openssl などのツールを使用できます。 サード パーティの CA またはツールを使用する方法については、使用しているソフトウェアのマニュアルを参照してください。

CA で証明書を作成するには、次の手順が含まれます。

1. 証明書テンプレートを構成するか、組織のドメインまたはセキュリティ管理者
2. または、組織のネットワーク コントローラーの管理者またはした SCVMM 管理者は、CA から新しい証明書を要求します。

#### <a name="certificate-configuration-requirements"></a>証明書の構成の要件

次の手順で、証明書テンプレートを構成するときに、テンプレートを構成するに次の必須の要素が含まれることを確認します。

1. 証明書のサブジェクト名は、Hyper-v ホストの FQDN である必要があります。
2. 証明書は、ローカル コンピューターの個人用ストアに配置する必要があります (マイ – cer \localmachine\my)
3. 証明書は両方のサーバー認証である必要があります (EKU: 1.3.6.1.5.5.7.3.1) とクライアント認証 (EKU: 1.3.6.1.5.5.7.3.2) アプリケーション ポリシー。

>[!NOTE]
>場合、個人用 \ (マイ – cert: \localmachine\my\) 証明書ストアに Hyper\ V ホストが 1 つ以上の X.509 証明書のサブジェクト名 (CN) との完全修飾ドメイン名 \(FQDN\) ホストとして、SDN によって使用される証明書に oid 1.3.6.1.4.1.311.95.1.1.1 追加のカスタム拡張キー使用法プロパティがあることを確認します。 それ以外の場合、ネットワーク コントローラーとホスト間の通信が動作しない可能性があります。

#### <a name="to-configure-the-certificate-template"></a>証明書テンプレートを構成するには
  
>[!NOTE]
>この手順を実行する前に、証明書の要件と、証明書テンプレート コンソールで使用可能な証明書テンプレートを確認する必要があります。 既存のテンプレートを変更するか、既存のテンプレートの複製を作成し、テンプレートのコピーを変更とします。 既存のテンプレートのコピーを作成することをお勧めします。

1. AD CS がインストールされている、サーバー マネージャーで、サーバーをクリックして**ツール**、] をクリックし、**証明機関**します。 証明機関の Microsoft 管理コンソール \(MMC\) を開きます。 
2. MMC で、ダブルクリック、CA の名前を右クリックして**証明書テンプレート**、] をクリックし、**管理**します。
3. 証明書テンプレート コンソールを開きます。 詳細ウィンドウで、すべての証明書テンプレートが表示されます。
4. 詳細ウィンドウで、複製するテンプレートをクリックします。
5.  をクリックして、**アクション**メニューで、クリックして**テンプレートの複製**します。 テンプレート**プロパティ**] ダイアログ ボックスが開きます。
6.  テンプレートで**プロパティ**] ダイアログ ボックスで、**サブジェクト名**] タブ、[ **、要求に含まれる**します。 \ (この設定は、ネットワーク コントローラーの SSL 証明書に必要です \)。
7.  テンプレートで**プロパティ**] ダイアログ ボックスで、**要求処理**] タブで、いることを確認**プライベート キーのエクスポートを許可する**が選択されています。 また必ず、**署名と暗号化**目的が選択されています。
8.  テンプレートで**プロパティ**] ダイアログ ボックスで、**拡張機能**] タブで、[**キー使用法**、] をクリックし、**編集**します。
9.  **署名**、いることを確認**デジタル署名**が選択されています。
10.  テンプレートで**プロパティ**] ダイアログ ボックスで、**拡張機能**] タブで、[**アプリケーション ポリシー**、] をクリックし、**編集**します。
11.  **アプリケーション ポリシー**、いることを確認**クライアント認証**と**サーバー認証**が一覧表示します。
12.  一意の名前で、証明書テンプレートのコピーを保存**ネットワーク コントローラー テンプレート**します。

#### <a name="to-request-a-certificate-from-the-ca"></a>CA から証明書を要求するには

証明書を要求する証明書スナップインを使用することができます。 任意の種類の事前に構成され、管理者は、CA 証明書の要求を処理するので利用可能にする証明書を要求できます。

**ユーザー**またはローカル**管理者**最小のグループ メンバーシップがこの手順を実行するために必要です。

1. コンピューターの証明書スナップインを開きます。
2. コンソール ツリーでクリックして**証明書 \(Local Computer\)**します。 選択、**個人**証明書ストアです。
3. **アクション**メニューをポイントし * * すべてのタスク * *、クリックして**新しい証明書の要求**証明書の登録ウィザードを開始します。 をクリックして**次**します。
4. 選択、**、管理者によって構成された**クリックして証明書登録ポリシー **[次へ]**します。
5. 選択、**Active Directory の登録ポリシー** \ (以前の section\ で構成されている CA テンプレートに基づく)。
6. 展開、**詳細**セクションし、次の項目を構成します。
    1. いることを確認**キー使用法**両方が含まれる * * デジタル署名 * * と**キーの暗号化**します。
    2. いることを確認**アプリケーション ポリシー**両方が含まれる**サーバー認証**\(1.3.6.1.5.5.7.3.1\) と**クライアント認証**\(1.3.6.1.5.5.7.3.2\) します。
7. をクリックして**プロパティ**します。
8. **サブジェクト**] タブの [**サブジェクト名**で、**種類**[**共通名**します。 [値] を指定**ネットワーク コントローラーの REST エンドポイント**します。
9. をクリックして**適用**、] をクリックし、**OK**します。
10. をクリックして**登録**します。

証明書スナップインで CA から登録した証明書の表示を個人用ストアをクリックします。

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>エクスポートと SCVMM ライブラリへの証明書のコピー

か、自己署名または CA\ の署名入り証明書を作成した後は、秘密キーで証明書をエクスポートする必要があります \(in.pfx format\) と秘密キーがない \ (で Base 64 の .cer 使用)、証明書スナップインからです。 

2 つのエクスポートされたファイルをコピーする必要があります、**ServerCertificate.cr**と**NCCertificate.cr** NC のサービス テンプレートをインポートする時に指定したフォルダーです。

1. (certlm.msc) 証明書スナップインを開き、ローカル コンピューターの個人証明書ストアに証明書を探します。
2. 証明書を右クリック] をクリックして**すべてのタスク**、] をクリックし、**エクスポート**します。 証明書のエクスポート ウィザードが開きます。 をクリックして**次**します。
3. 選択**はい**、秘密キーのオプションのエクスポート] をクリックして**[次へ]**します。
4. 選択**Personal Information Exchange - PKCS #12 (.PFX)**に既定の設定をそのまま使用し、**証明のパスのすべての証明書を含める**可能な場合です。
5. ユーザー/グループおよびエクスポートするには、証明書のパスワードを割り当てる] をクリックして**次**します。
6. ページをエクスポートするファイルで、エクスポートされたファイルを配置する場所を参照し、名前を付けします。
7. 同様に、証明書をエクスポートします。CER フォーマットします。 注: エクスポートするのには。CER 形式で、[はい] をオフに、プライベート キーのオプションをエクスポートします。
8. コピーします。ServerCertificate.cr フォルダーに PFX です。
9. コピーします。NCCertificate.cr フォルダーへの CER ファイル。

完了したら、SCVMM ライブラリでこれらのフォルダーを更新し、これらの証明書は、コピーがあることを確認します。 ネットワーク コントローラーのサービス テンプレートの構成と展開を続行します。

## <a name="authenticating-southbound-devices-and-services"></a>Southbound デバイスとサービスの認証 

ホストと SLB MUX デバイスとネットワーク コントローラーの通信は、認証の証明書を使用します。 ホストとの通信は OVSDB プロトコル経由では SLB MUX デバイスとの通信が WCF プロトコル上にあるときです。

### <a name="hyper-v-host-communication-with-network-controller"></a>ネットワーク コントローラーとの通信を使用した hyper-v ホスト

OVSDB 経由での Hyper-V ホストとの通信、ネットワーク コントローラーをホスト コンピューターに証明書を提示する必要があります。 既定では、SCVMM は、ネットワーク コントローラーで構成されている SSL 証明書を選択し、ホストと southbound の通信に使用します。

SSL 証明書にクライアント認証の EKU が構成されている必要がありますがある理由理由です。 この証明書が「サーバー」の残りの部分で構成されているリソース \ (Hyper-V ホストとして表されますネットワーク コントローラーでサーバー resource\)、Windows PowerShell コマンドを実行して表示できます**Get NetworkControllerServer**します。

サーバー REST リソースの部分的な例を次に示します。

      "resourceId": "host31.fabrikam.com",
      "properties": {
        "connections": [
          {
            "managementAddresses": [
               "host31.fabrikam.com"
            ],
            "credential": {
              "resourceRef": "/credentials/a738762f-f727-43b5-9c50-cf82a70221fa"
            },
            "credentialType": "X509Certificate"
          }
        ],

相互認証は、Hyper-V ホストは、ネットワーク コントローラーと通信するために証明書を必要もあります。 

証明機関 \(CA\) から証明書を登録することができます。 ホスト コンピューター ベースの CA 証明書が見つからない場合、SCVMM は自己署名証明書を作成し、それをホスト コンピューターのプロビジョニングします。

ネットワーク コントローラーと Hyper-V ホストの証明書は、互いから信頼されている必要があります。 Hyper-V ホストの証明書のルート証明書に存在する必要があります、ローカル コンピューター、またはその逆に、ネットワーク コントローラー信頼されたルート証明機関が格納されます。 

自己署名証明書を使用している SCVMM は必要な証明書がローカル コンピューターの信頼されたルート証明機関ストアに存在することを確認します。 

Hyper-V ホストをベースの CA 証明書を使用している場合は、ローカル コンピューターのネットワーク コントローラーの信頼されたルート証明機関ストアにルート CA 証明書があることを確認する必要があります。

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>ネットワーク コントローラーとソフトウェア ロード バランサー マルチプレクサー通信

ソフトウェア ロード バランサー マルチプレクサー \(MUX\) とネットワーク コントローラーの認証証明書を使用して、WCF プロトコル経由で通信します。

既定では、SCVMM は、ネットワーク コントローラーで構成されている SSL 証明書を選択し、Mux デバイスと southbound の通信に使用します。 この証明書が"NetworkControllerLoadBalancerMux"で構成されているリソースを移動し、Powershell コマンドレットを実行して表示できる**Get NetworkControllerLoadBalancerMux**します。

MUX REST リソース \(partial\) の例:

      "resourceId": "slbmux1.fabrikam.com",
      "properties": {
        "connections": [
          {
            "managementAddresses": [
               "slbmux1.fabrikam.com"
            ],
            "credential": {
              "resourceRef": "/credentials/a738762f-f727-43b5-9c50-cf82a70221fa"
            },
            "credentialType": "X509Certificate"
          }
        ],

相互認証は、SLB MUX デバイスで証明書を必要することもあります。 この証明書が自動的に構成 SCVMM SCVMM を使用して、ソフトウェア ロード バランサーを展開するときにします。

>[!IMPORTANT]
>ホストと SLB ノードでは重要なすべての証明書が信頼されたルート証明機関の証明書ストアに含まれていないこと」に発行"場所は「発行元」と同じです。 このような場合は、ネットワーク コントローラーと southbound のデバイス間の通信が失敗します。

他のによって、ネットワーク コントローラーと SLB MUX 証明書が信頼されている必要があります \ (、SLB MUX 証明書のルート証明書は信頼されたルート証明機関のストアと副 versa\、ネットワーク コントローラーのコンピューターに存在である必要があります)。 SCVMM により、必要な証明書に存在する自己署名証明書を使用しているときに、信頼されたルート証明機関で、ローカル コンピューターに保存します。



