---
title: SDN の Internal DNS Service (iDNS)
description: このトピックでは、Windows Server 2016 のソフトウェア定義ネットワークと統合されている内部 DNS (Idn) を使用して、ホストされているテナントワークロードに DNS サービスを提供する方法について説明します。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: ad848a5b-0811-4c67-afe5-6147489c0384
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 47765dc6a08821b0b7032261467bef78239f8369
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520251"
---
# <a name="internal-dns-service-idns-for-sdn"></a>SDN の Internal DNS Service (iDNS)

>適用先:Windows Server (半期チャネル)、Windows Server 2016

\( \) Windows Server 2016 でソフトウェアによるネットワーク SDN の展開を計画しているクラウドサービスプロバイダーの CSP またはエンタープライズの場合は \( \) 、 \( \) SDN と統合された内部 dns idn を使用して、ホストされているテナントのワークロードに dns サービスを提供できます。

ホストされた仮想マシン \( \) の vm とアプリケーションは、自身のネットワーク内およびインターネット上の外部リソースと通信するために DNS を必要とします。 Idn を使用すると、テナントは、分離されたローカルの名前空間とインターネットリソースに対して DNS 名前解決サービスを提供できます。

Idn プロキシを経由するのではなく、テナントの仮想ネットワークから Idn サービスにアクセスできないため、テナントネットワーク上の悪意のあるアクティビティに対してサーバーが脆弱になることはありません。

**主要機能**

Idn の主な機能を次に示します。

- テナントワークロードの共有 DNS 名前解決サービスを提供します
- 名前解決と DNS 登録のための権限のある DNS サービス (テナント名空間内)
- テナントの VM からインターネット名を解決する再帰的な DNS サービス。
- 必要に応じて、ファブリック名とテナント名の同時ホストを構成できます。
- コスト効果の高い DNS ソリューション-テナントは独自の DNS インフラストラクチャを展開する必要はありません。
- Active Directory 統合を使用した高可用性。これは必須です。

これらの機能に加えて、AD 統合 DNS サーバーをインターネットに対して開いたままにすることが懸念される場合は、境界ネットワーク内の別の再帰的なリゾルバーの背後に Idn サーバーを展開できます。

Idn はすべての DNS クエリに対して集中管理されたサーバーであるため、CSP またはエンタープライズは、テナント DNS ファイアウォールの実装、フィルターの適用、悪意のあるアクティビティの検出、および集中管理された場所でのトランザクションの監査も行うことができます。

## <a name="idns-infrastructure"></a>Idn インフラストラクチャ
Idn インフラストラクチャには、Idn サーバーと Idn プロキシが含まれています。

### <a name="idns-servers"></a>Idn サーバー
Idn には、VM DNS リソースレコードなど、テナント固有のデータをホストする一連の DNS サーバーが含まれています。

iDNS サーバーは、それの内部 DNS ゾーンの権限を持つサーバーであり、テナント VM が外部リソースに接続するときのパブリック名のリゾルバーとして機能します。

仮想ネットワーク上の Vm のホスト名はすべて、同じゾーンに DNS リソースレコードとして保存されます。 たとえば、contoso. local という名前のゾーンに対して Idn を展開する場合、そのネットワーク上の Vm の DNS リソースレコードは、contoso. ローカルゾーンに格納されます。

テナント VM の完全修飾ドメイン名 \( fqdn \) は、コンピューター名と VIRTUAL NETWORK の DNS サフィックス文字列 (GUID 形式) で構成されます。 たとえば、Virtual Network contoso, local という名前のテナント VM がある場合、VM の FQDN は TENANT1 です。*vn*を指定します。 *vn*は、Virtual Network の DNS サフィックス文字列です。

>[!NOTE]
>ファブリック管理者は、Idn サーバーとして使用するために特別に使用する新しい DNS サーバーを展開するのではなく、CSP サーバーまたはエンタープライズ DNS インフラストラクチャを Idn サーバーとして使用できます。 Idn 用の新しいサーバーを展開するか、既存のインフラストラクチャを使用するかにかかわらず、Idn は Active Directory を利用して高可用性を実現します。 したがって、Idn サーバーは Active Directory に統合されている必要があります。

### <a name="idns-proxy"></a>Idn プロキシ
Idn プロキシは、すべてのホストで実行される Windows サービスであり、テナント Virtual Network DNS トラフィックを Idn サーバーに転送します。

次の図は、idn プロキシ経由で Idn サーバーとインターネットに接続しているテナント仮想ネットワークからの DNS トラフィックパスを示しています。

![Idn インフラストラクチャ](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Idn を展開する方法
スクリプトを使用して Windows Server 2016 で SDN を展開すると、Idn が自動的に展開に含まれるようになります。

詳細については、次の各トピックを参照してください。

- [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開する](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Idn の展開手順について
このセクションを使用すると、スクリプトを使用して SDN を展開するときに Idn をインストールし、構成する方法を理解することができます。

Idn を展開するために必要な手順の概要を次に示します。

>[!NOTE]
>スクリプトを使用して SDN を展開した場合は、次の手順を実行する必要はありません。 ここで説明する手順は、情報とトラブルシューティングのみを目的として提供されています。

### <a name="step-1-deploy-dns"></a>手順 1: DNS を展開する
DNS サーバーを展開するには、次の Windows PowerShell コマンド例を使用します。

```powershell
Install-WindowsFeature DNS -IncludeManagementTools
```

### <a name="step-2-configure-idns-information-in-network-controller"></a>手順 2: ネットワークコントローラーで Idn 情報を構成する
このスクリプトセグメントは、管理者がネットワークコントローラーに対して実行する REST 呼び出しであり、Idn ゾーン構成 (iDNSServer の IP アドレスや Idn 名のホストに使用されるゾーンなど) について通知します。

```
Url: https://<url>/networking/v1/iDnsServer/configuration
Method: PUT
{
      "properties": {
        "connections": [
          {
            "managementAddresses": [
              "10.0.0.9"
            ],
            "credential": {
              "resourceRef": "/credentials/iDnsServer-Credentials"
            },
            "credentialType": "usernamePassword"
          }
        ],
        "zone": "contoso.local"
      }
    }
```

>[!NOTE]
>これは SDNExpress.ps1 のセクション**Configuration ConfigureIDns**から抜粋したものです。 詳細については、「[Deploy a Software Defined Network infrastructure using scripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)」 (スクリプトを使用してソフトウェアによるネットワーク制御インフラストラクチャを展開する) を参照してください。

### <a name="step-3-configure-the-idns-proxy-service"></a>手順 3: Idn プロキシサービスを構成する
Idn プロキシサービスは各 Hyper-v ホスト上で実行され、テナントの仮想ネットワークと Idn サーバーが配置されている物理ネットワークとの間にブリッジを提供します。 次のレジストリキーは、すべての Hyper-v ホスト上に作成する必要があります。

**DNS ポート:** 固定ポート53

- レジストリキー = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- ValueName = "Port"
- ValueData = 53
- ValueType = "Dword"

**DNS プロキシポート:** 固定ポート53

- レジストリキー = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- ValueName = "ProxyPort"
- ValueData = 53
- ValueType = "Dword"

**DNS IP:** テナントが Idn サービスを使用することを選択した場合に、ネットワークインターフェイスで構成された固定 IP アドレス

- レジストリキー = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- ValueName = "IP"
- ValueData = "169.254.169.254"
- ValueType = "String"

**Mac アドレス:** DNS サーバーのメディア Access Control アドレス

- レジストリキー = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService
- ValueName = "MAC"
- ValueData = "aa-bb-cc-bb-cc"
- ValueType = "String"

**Idn サーバーアドレス:** Idn サーバーのコンマ区切りの一覧。

- レジストリキー: HKLM\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- ValueName = "フォワーダー"
- ValueData = "10.0.0.9"
- ValueType = "String"

>[!NOTE]
>これは SDNExpress.ps1 のセクション**Configuration ConfigureIDnsProxy**から抜粋したものです。 詳細については、「[Deploy a Software Defined Network infrastructure using scripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)」 (スクリプトを使用してソフトウェアによるネットワーク制御インフラストラクチャを展開する) を参照してください。

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>手順 4: ネットワークコントローラーのホストエージェントサービスを再起動する
次の Windows PowerShell コマンドを使用して、ネットワークコントローラーのホストエージェントサービスを再起動できます。

```powershell
Restart-Service nchostagent -Force
```

詳細については、「 [Restart-Service](https://technet.microsoft.com/library/hh849823.aspx)」を参照してください。

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>DNS プロキシサービスのファイアウォール規則を有効にする
次の Windows PowerShell コマンドを使用して、プロキシが VM と Idn サーバーと通信するための例外を許可するファイアウォール規則を作成できます。

```powershell
Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'
```

詳細については、「 [set-netfirewallrule](https://technet.microsoft.com/library/jj554869.aspx)」を参照してください。

### <a name="validate-the-idns-service"></a>Idn サービスを検証する
Idn サービスを検証するには、サンプルのテナントワークロードをデプロイする必要があります。

詳細については、「 [VM の作成とテナント Virtual Network または VLAN への接続](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)」を参照してください。

テナント VM で Idn サービスを使用する場合は、VM ネットワークインターフェイスの DNS サーバー構成を空白のままにして、インターフェイスで DHCP を使用できるようにする必要があります。

このようなネットワークインターフェイスを持つ VM が開始されると、vm が Idn を使用できるように構成が自動的に受信され、VM は Idn サービスを使用して名前解決の実行を直ちに開始します。

ネットワークインターフェイスの DNS サーバーと代替 DNS サーバー情報を空にして、Idn サービスを使用するようにテナント VM を構成した場合、ネットワークコントローラーは VM に IP アドレスを提供し、Idn サーバーとの VM に代わって DNS 名の登録を実行します。

また、ネットワークコントローラーは、vm の名前解決を実行するために必要な詳細情報を Idn プロキシに伝えます。

VM が DNS クエリを開始すると、プロキシは、Virtual Network から Idn サービスへのクエリのフォワーダーとして機能します。

また、DNS プロキシによって、テナント VM のクエリが分離されます。 Idn サーバーがクエリに対して権限を持っている場合、Idn サーバーは権限のある応答で応答します。 Idn サーバーがクエリに対して権限を持っていない場合、インターネット名を解決するために DNS 再帰が実行されます。

>[!NOTE]
>この情報は SDNExpressTenant.ps1 の「 **Configuration AttachToVirtualNetwork** 」セクションに記載されています。 詳細については、「[Deploy a Software Defined Network infrastructure using scripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)」 (スクリプトを使用してソフトウェアによるネットワーク制御インフラストラクチャを展開する) を参照してください。

