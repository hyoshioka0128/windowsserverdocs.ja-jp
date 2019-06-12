---
title: ソフトウェアによるネットワーク制御の証明書を管理します。
description: このトピックを使用すると、ソフトウェア定義ネットワーク (SDN) で Windows Server 2016 Datacenter を展開するときに、ネットワーク コント ローラーの Northbound と Southbound 通信の証明書を管理するのに方法について説明します。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: d29a98e24b475c38fee61972bf9efbd5a2528974
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446261"
---
# <a name="manage-certificates-for-software-defined-networking"></a>ソフトウェアによるネットワーク制御の証明書を管理します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用するには、ソフトウェアによるネットワーク制御を展開するときに、ネットワーク コント ローラーの Northbound と Southbound 通信用の証明書を管理する方法について\(SDN\)システムを使用すると Windows Server 2016 DatacenterVirtual Machine Manager の中央\(SCVMM\) SDN 管理クライアントとして。

>[!NOTE]
>ネットワーク コント ローラーの概要については、次を参照してください。[ネットワーク コント ローラー](../technologies/network-controller/Network-Controller.md)します。

ネットワーク コント ローラーの通信を保護する Kerberos を使用していない場合は、認証、承認、および暗号化の X.509 証明書を使用できます。

Windows Server 2016 Datacenter での SDN は、両方の自己をサポートしています\-署名と証明機関\(CA\)-X.509 証明書を署名します。 このトピックでは、ソフトウェアなどのネットワーク デバイスの管理クライアントでネットワーク コント ローラーの Northbound 通信チャネルをセキュリティで保護するこれらの証明書を作成し、適用するための手順と Southbound 通信を提供します。ロード バランサー \(SLB\)します。
.
証明書を使用しているときに\-ベースの認証では、次の方法で使用されているネットワーク コント ローラーのノードで 1 つ証明書を登録する必要があります。

1. Secure Sockets Layer の Northbound 通信を暗号化\(SSL\)ネットワーク コント ローラーのノードと、System Center Virtual Machine Manager などの管理クライアントの間。
2. ネットワーク コント ローラーのノードと Southbound のデバイスと、HYPER-V ホストやソフトウェア ロード バランサーなどのサービス間認証\(SLBs\)します。

## <a name="creating-and-enrolling-an-x509-certificate"></a>作成して、X.509 証明書の登録

作成して登録するか、自己\-証明書または CA によって発行される証明書に署名します。

>[!NOTE]
>SCVMM を使用して、ネットワーク コント ローラーをデプロイする場合は、ネットワーク コント ローラーのサービス テンプレートの構成中に Northbound 通信を暗号化するために使用される X.509 証明書を指定する必要があります。

証明書の構成には、次の値を含める必要があります。

- 値、 **RestEndPoint**テキスト ボックスでは、ネットワーク コント ローラー完全修飾ドメイン名をする必要がありますか\(FQDN\)または IP アドレス。 
- **RestEndPoint**値は、サブジェクト名と一致する必要があります\(共通名、CN\) X.509 証明書。

### <a name="creating-a-self-signed-x509-certificate"></a>自動作成\-X.509 証明書の署名

自己署名 X.509 証明書を作成し、秘密キーと共にエクスポート\(パスワードで保護\)次の 1 つの手順に従って\-ノードと複数\-ネットワーク コント ローラーのノードの展開.

作成自己\-署名証明書は、次のガイドラインを使用することができます。

- DnsName パラメーター - ネットワーク コント ローラーの REST エンドポイントの IP アドレスを使用できますが、これは使用しないで、ネットワーク コント ローラーのノードがすべて、1 つの管理サブネット内にある必要があるため\(単一のラックの例。\)
- 指定した DNS 名には複数の NC ノードの展開、ネットワーク コント ローラー クラスターの FQDN になります\(DNS ホストの A レコードが自動的に作成します。\) 
- 単一ノード ネットワーク コント ローラーの展開では、DNS 名は、ネットワーク コント ローラーのホスト名の後に完全なドメイン名を指定できます。

#### <a name="multiple-node"></a>複数のノード

使用することができます、 [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell コマンドの自動作成を\-証明書に署名します。

**構文**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**使用例**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>1 つのノード

使用することができます、 [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell コマンドの自動作成を\-証明書に署名します。

**構文**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**使用例**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>CA を作成する\-X.509 証明書の署名

を CA を使用して、証明書を作成する必要がありますが既に展開して、公開キー基盤\(PKI\) Active Directory 証明書サービス\(AD CS\)します。 

>[!NOTE]
>ただし、このトピックの手順では、AD CS に固有、ネットワーク コント ローラーを使用する証明書を作成する、サード パーティの Ca または、openssl などのツールを使用できます。 サード パーティの CA またはツールを使用する方法については、使用しているソフトウェアのマニュアルを参照してください。

CA の証明書を作成するには、次の手順が含まれます。

1. または、組織のドメインやセキュリティ管理者は、証明書テンプレートを構成します。
2. ユーザーまたは組織のネットワーク コント ローラーの管理者または SCVMM 管理者は、CA から新しい証明書を要求します。

#### <a name="certificate-configuration-requirements"></a>証明書の構成の要件

次の手順で証明書テンプレートを構成するときにを構成するテンプレートに次の必須の要素が含まれていることを確認します。

1. 証明書のサブジェクト名は、HYPER-V ホストの FQDN である必要があります。
2. ローカル コンピューターの個人用ストアに証明書を配置する必要があります (私 – \localmachine\my)
3. 証明書の両方のサーバー認証が必要 (EKU:1.3.6.1.5.5.7.3.1) とクライアント認証 (EKU:1.3.6.1.5.5.7.3.2) アプリケーション ポリシー。

>[!NOTE]
>場合、個人\(– マイ \localmachine\my\)証明書ストアに、ハイパー\-V ホストがホストの完全修飾ドメイン名としては、複数の X.509 証明書のサブジェクト名 (CN) を持つ\(FQDN\)、SDN により使用される証明書に OID 1.3.6.1.4.1.311.95.1.1.1 で追加のカスタム拡張キー使用法プロパティがあることを確認します。 それ以外の場合、ネットワーク コント ローラーとホスト間の通信は動作しない可能性があります。

#### <a name="to-configure-the-certificate-template"></a>証明書テンプレートを構成するには
  
>[!NOTE]
>この手順を実行する前に、証明書の要件と、証明書テンプレート コンソールで使用できる証明書テンプレートを確認する必要があります。 既存テンプレートを変更か、既存のテンプレートの複製を作成し、テンプレートのコピーを変更とします。 既存のテンプレートのコピーを作成することをお勧めします。

1. AD CS がインストールされている、サーバー マネージャーで、サーバーで次のようにクリックします。**ツール**、 をクリックし、**証明機関**します。 証明機関の Microsoft 管理コンソール\(MMC\)が開きます。 
2. MMC で、CA の名前をダブルクリック、右クリック**証明書テンプレート**、 をクリックし、**管理**します。
3. 証明書テンプレート コンソールを開きます。 詳細ウィンドウでは、すべての証明書テンプレートが表示されます。
4. 詳細ペインで、複製するテンプレートをクリックします。
5.  をクリックして、**アクション** メニューをクリック**テンプレートの複製**します。 テンプレート**プロパティ** ダイアログ ボックスが表示されます。
6.  テンプレートで**プロパティ**] ダイアログ ボックスの [、**サブジェクト名**] タブで [**要求に含まれる**します。 \(この設定は、ネットワーク コント ローラーの SSL 証明書に必要です。\)
7.  テンプレートで**プロパティ** ダイアログ ボックスで、**要求処理** タブで、いることを確認**をエクスポートする秘密キーを許可する**が選択されています。 いることを確認、**署名と暗号化**目的を選択します。
8.  テンプレートで**プロパティ**] ダイアログ ボックスの [、**拡張**] タブで [**キー使用法**、順にクリックします**編集**。
9.  **署名**、いることを確認**デジタル署名**が選択されています。
10.  テンプレートで**プロパティ**] ダイアログ ボックスの [、**拡張**] タブで [**アプリケーション ポリシー**、順にクリックします**編集**。
11.  **アプリケーション ポリシー**、いることを確認**クライアント認証**と**サーバー認証**一覧表示されます。
12.  一意の名前で証明書テンプレートのコピーを保存**ネットワーク コント ローラー テンプレート**します。

#### <a name="to-request-a-certificate-from-the-ca"></a>CA から証明書を要求するには

証明書を要求する証明書スナップインを使用することができます。 任意の種類の事前構成済みおよび証明書の要求を処理する CA の管理者によって利用された証明書を要求できます。

**ユーザー**またはローカル**管理者**はこの手順を実行するために必要な最小のグループ メンバーシップになります。

1. コンピューターの証明書スナップインを開きます。
2. コンソール ツリーで、クリックして**証明書\(ローカル コンピューター\)** します。 選択、**個人**証明書ストア。
3. **アクション**メニューで、* * すべてのタスク<strong>、順にクリックします * * 新しい証明書の要求</strong>証明書の登録ウィザードを起動します。 **[次へ]** をクリックします。
4. 選択、 **、管理者によって構成**証明書登録ポリシーをクリックします**次**します。
5. 選択、 **Active Directory 登録ポリシー** \(前のセクションで構成されている CA テンプレートに基づく\)します。
6. 展開、**詳細**セクションし、次の項目を構成します。
   1. いることを確認**キー使用法**両方が含まれる<strong>デジタル署名 * * と * * キーの暗号化</strong>します。
   2. いることを確認**アプリケーション ポリシー**両方が含まれる**サーバー認証** \(1.3.6.1.5.5.7.3.1\)と**クライアント認証**\(1.3.6.1.5.5.7.3.2\)します。
7. **[プロパティ]** を選択します。
8. **サブジェクト**] タブの [**サブジェクト名**の**型**を選択します**共通名**します。 値は、次のように指定します。**ネットワーク コント ローラーの REST エンドポイント**します。
9. **[適用]** をクリックし、 **[OK]** をクリックします。
10. **[登録]** をクリックします。

証明書スナップインで、CA から登録した証明書の表示を個人用ストアをクリックします。

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>エクスポートして、SCVMM ライブラリへの証明書のコピー

いずれか、自己の作成後\-署名または CA\-署名入り証明書、秘密キーで証明書をエクスポートする必要があります\(.pfx 形式で\)と秘密キーのない\(Base 64 の .cer 形式で\)証明書スナップインから。 

2 つのエクスポートされたファイルをコピーする必要がありますし、 **ServerCertificate.cr**と**NCCertificate.cr** NC サービス テンプレートをインポートしたときに、時に指定したフォルダーです。

1. 証明書スナップイン (certlm.msc) を開くし、ローカル コンピューターの個人証明書ストアに証明書を見つけます。
2. 右\-証明書をクリックし**すべてのタスク**、 をクリックし、**エクスポート**します。 証明書のエクスポート ウィザードが開きます。 **[次へ]** をクリックします。
3. 選択**はい**エクスポート秘密キーのオプションをクリックし、**次**。
4. 選択**Personal Information Exchange - PKCS #12 (します。PFX)** に既定の設定をそのまま使用し、**証明のパスにすべての証明書を含む**可能な場合。
5. ユーザー/グループをエクスポートする証明書のパスワードの割り当て をクリックして**次**します。
6. ページをエクスポートするファイルで、エクスポートされたファイルを配置する場所を参照し、名前を付けます。
7. 同様に、証明書をエクスポートします。CER 形式です。 注:エクスポートします。CER 形式は、[はい] をオフに、秘密キーのオプションをエクスポートします。
8. コピーします。PFX を ServerCertificate.cr フォルダーにします。
9. コピーします。CER ファイルを NCCertificate.cr フォルダーにします。

完了したら、SCVMM ライブラリでこれらのフォルダーを更新し、コピーこれらの証明書があることを確認します。 ネットワーク コント ローラー サービス テンプレートの構成と展開を続行します。

## <a name="authenticating-southbound-devices-and-services"></a>認証 Southbound デバイスおよびサービス認証 

ホストと SLB MUX のデバイスをネットワーク コント ローラーの通信には、認証用証明書が使用されます。 ホストとの通信は OVSDB プロトコル経由で SLB MUX デバイスとの通信は WCF プロトコルです。

### <a name="hyper-v-host-communication-with-network-controller"></a>ネットワーク コント ローラーとの通信を HYPER-V ホスト

OVSDB 上の HYPER-V ホストとの通信をネットワーク コント ローラーは、ホスト コンピューターに証明書を提示する必要があります。 既定では、SCVMM は、ネットワーク コント ローラーに構成されている SSL 証明書を取得され、ホストとの southbound 通信に使用します。

理由の SSL 証明書が構成されているクライアント認証 EKU に理由が必要です。 この証明書が「サーバー」残りの部分で構成されているリソース\(HYPER-V ホストがサーバーのリソースとネットワーク コント ローラーで表される\)、Windows PowerShell のコマンドを実行して表示できます**Get NetworkControllerServer**します。

サーバーの REST リソースの部分的な例を次に示します。

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

相互認証は、HYPER-V ホストは、ネットワーク コント ローラーとの通信に証明書を必要もあります。 

証明機関から証明書を登録する\(CA\)します。 ホスト コンピューターで、ベースの CA 証明書が見つからない場合、SCVMM は自己署名証明書を作成し、ホスト コンピューターをプロビジョニングします。

ネットワーク コント ローラーと HYPER-V ホストの証明書は、他のによって信頼する必要があります。 HYPER-V ホストの証明書のルート証明書が必要であるネットワーク コント ローラー信頼されたルート証明機関は、ローカルのコンピューターでは、その逆を格納します。 

使用すると、自己\-署名証明書、SCVMM により必要な証明書がローカル コンピューターの信頼されたルート証明機関ストアに存在するようになります。 

HYPER-V ホストのベースの CA 証明書を使用する場合は、CA ルート証明書がローカル コンピューターのネットワーク コント ローラーの信頼されたルート証明機関ストアに存在することを確認する必要があります。

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>ネットワーク コント ローラーとソフトウェア ロード バランサー MUX 通信

ソフトウェア ロード バランサー マルチプレクサー \(MUX\)と WCF プロトコルでは、ネットワーク コント ローラー通信証明書認証を使用します。

既定では、SCVMM は、ネットワーク コント ローラーに構成されている SSL 証明書を取得し、Mux デバイスとの southbound 通信に使用します。 この証明書が"NetworkControllerLoadBalancerMux"で構成されているリソースを移動し、Powershell コマンドレットを実行して表示できる**Get NetworkControllerLoadBalancerMux**。

MUX REST リソースの例\(部分\):

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

相互認証は、SLB MUX のデバイスで証明書を必要することもあります。 SCVMM を使用して、ソフトウェア ロード バランサーをデプロイするときに、SCVMM でこの証明書が自動的に構成します。

>[!IMPORTANT]
>ホストと SLB ノードでは重要な任意の証明書が信頼されたルート証明機関の証明書ストアに含まれていないことを「発行先」は「発行元」と同じです。 この場合、ネットワーク コント ローラーと southbound のデバイス間の通信は失敗します。

他の各ネットワーク コント ローラーと SLB MUX の証明書を信頼する必要が\(SLB MUX の証明書のルート証明書は、ネットワーク コント ローラー マシンの信頼されたルート証明機関ストアに存在する必要があります、またはその逆\)します。 自己を使っている場合\-署名証明書、SCVMM は確実に必要な証明書が指定されている、ローカル コンピューターのストアに信頼されたルート証明機関。



