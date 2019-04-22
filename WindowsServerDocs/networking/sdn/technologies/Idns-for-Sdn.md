---
title: SDN の Internal DNS Service (iDNS)
description: このトピックでは、Windows Server 2016 でソフトウェアによるネットワーク制御と統合されている内部 DNS (Idn) を使用して、ホストされているテナントのワークロードに DNS サービスを提供する方法について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ad848a5b-0811-4c67-afe5-6147489c0384
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4d4ae5ee5f5600d86349ca26b7acbdb284b45bac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824083"
---
# <a name="internal-dns-service-idns-for-sdn"></a>SDN の Internal DNS Service (iDNS)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

クラウド サービス プロバイダーに作業している場合\(CSP\)またはソフトウェアによるネットワーク制御の展開を計画しているエンタープライズ\(SDN\) Windows Server 2016 では、ホストされているテナント ワークロードを DNS サービスを行うことができます内部 DNS を使用して\(Idn\)SDN と統合されています。

仮想マシンがホストされている\(Vm\)アプリケーションには、独自のネットワーク内およびインターネット上の外部のリソースを通信するために DNS が必要とします。 Idn を使用できますは、ローカルの分離された名前空間のとインターネット リソースの DNS 名前解決サービスでテナントを提供します。

Idn サービスにテナント仮想ネットワークからアクセスできないため、以外の Idn プロキシを介してサーバーでないテナント ネットワークに悪意のあるアクティビティに対して脆弱になります。

**主な機能**

Idn の主な機能を次に示します。

- 共有 DNS 名前解決サービス テナントのワークロードを提供します。
- 名前解決およびテナントの名前空間内での DNS 登録の権限のある DNS サービス
- 再帰 DNS サービスのテナントの Vm からインターネット名前解決。
- ファブリックとテナントの名前の同時ホストを構成するには、必要な場合
- コスト効率の高い DNS ソリューションでは、独自の DNS インフラストラクチャをデプロイするテナントは必要はありません。
- Active Directory の統合により、必要とされる高可用性。

これらの機能に加えて DNS サーバーを開くには、インターネットに、AD の統合を維持する心配がある場合、境界ネットワーク内の別の再帰リゾルバーの背後にある Idn サーバーを展開することができます。

IDNS はすべての DNS クエリの一元的なサーバーであるため、CSP またはエンタープライズできますもテナント DNS ファイアウォールを実装、フィルターを適用、悪意のあるアクティビティを検出および中央の場所でのトランザクションの監査

## <a name="idns-infrastructure"></a>Idn インフラストラクチャ
Idn インフラストラクチャには、Idn サーバーと Idn のプロキシが含まれています。

### <a name="idns-servers"></a>Idn サーバー
Idn には、一連 VM の DNS リソース レコードなど、テナント固有のデータをホストする DNS サーバーにはが含まれています。

Idn サーバーの権限のあるサーバーの内部の DNS ゾーンとパブリック名の競合回避モジュールとしても機能とテナントの Vm の外部リソースへの接続を試行します。

すべての仮想ネットワーク上の Vm のホスト名は、同じゾーンで DNS リソース レコードとして格納されます。 たとえば、contoso.local という名前のゾーン用の iDNS を展開する場合は、そのネットワーク上の Vm の DNS リソース レコードが、contoso.local ゾーンに格納されます。

VM の完全修飾ドメイン名をテナント\(Fqdn\) GUID 形式で、仮想ネットワークのコンピューター名と DNS サフィックス文字列で構成されます。 たとえば、テナントの仮想ネットワーク contoso では、ローカルの上にある TENANT1 という名前の VM がある場合、VM の FQDN は TENANT1 します。*vn guid*. contoso.local、、 *vn guid*仮想ネットワークの DNS サフィックスの文字列は、します。

>[!NOTE]
>ファブリック管理者の場合は、Idn としてサーバーを使用して専用の新しい DNS サーバーを展開するのではなく、Idn サーバーとして、CSP または企業の DNS インフラストラクチャを使用できます。 Idn の新しいサーバーを展開する場合も、既存のインフラストラクチャを使用して、Idn は高可用性を提供する Active Directory に依存します。 Idn サーバーは、Active Directory したがって統合する必要があります。

### <a name="idns-proxy"></a>プロキシの iDNS
Idn プロキシは、すべてのホスト上で実行されると、テナント Idn サーバーへの仮想ネットワークの DNS トラフィックを転送する Windows サービスです。

次の図は、Idn プロキシ Idn サーバーを使ったテナントの仮想ネットワークとインターネットからの DNS トラフィックのパスを示しています。

![Idn インフラストラクチャ](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Idn をデプロイする方法
スクリプトを使用して Windows Server 2016 の SDN を展開するときに、展開で Idn が自動的に含まれます。

詳しくは、次のトピックをご覧ください。

- [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイします。](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Idn の配置手順を理解します。
このセクションを使用すると、Idn がインストールされ、スクリプトを使用して SDN を展開するときに構成する方法を理解します。

Idn の展開に必要な手順の概要を次に示します。

>[!NOTE]
>スクリプトを使用して SDN を展開する場合は、次の手順を実行する必要はありません。 手順は、情報とトラブルシューティングの目的でのみ提供されます。

### <a name="step-1-deploy-dns"></a>手順 1:DNS を展開します。
DNS サーバーを展開するには、次の例の Windows PowerShell コマンドを使用します。
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>手順 2:ネットワーク コント ローラーで Idn の情報を構成します。
このスクリプトのセグメントは、REST 呼び出しが行われる、管理者がネットワーク コント ローラーに Idn ゾーンの構成 -、iDNSServer および Idn 名をホストするために使用するゾーンの IP アドレスなどに関する通知です。 

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
>これは、セクションからの抜粋**構成 ConfigureIDns** SDNExpress.ps1 でします。 詳細については、次を参照してください。[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイ](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)します。

### <a name="step-3-configure-the-idns-proxy-service"></a>手順 3:Idn プロキシ サービスを構成します。
Idn プロキシ サービスは、各テナントの仮想ネットワークと Idn サーバーが配置される、物理ネットワーク間のブリッジを提供する、HYPER-V ホストで実行されます。 すべての HYPER-V ホストでは、次のレジストリ キーを作成する必要があります。


**DNS のポート:** 固定ポート 53

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName「ポート」を =
- ValueData 53 を =
- ValueType = "Dword"
       

**DNS プロキシ ポート:** 固定ポート 53

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "ProxyPort"
- ValueData 53 を =
- ValueType = "Dword"
        
**DNS の IP アドレス:** テナントが Idn サービスを使用した場合に、ネットワーク インターフェイスで構成されている固定の IP アドレス

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName"IP"を =
- ValueData「169.254.169.254」を =
- ValueType ="String"

        
**Mac アドレス:** DNS サーバーのメディア アクセス制御アドレス

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService
- ValueName = "MAC"
- ValueData = “aa-bb-cc-aa-bb-cc”
- ValueType ="String"

**IDN サーバーのアドレス:** コンマ区切りの Idn サーバーの一覧。

- レジストリ キー: HKLM\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- ValueName「フォワーダー」を =
- ValueData「10.0.0.9」を =
- ValueType ="String"



>[!NOTE]
>これは、セクションからの抜粋**構成 ConfigureIDnsProxy** SDNExpress.ps1 でします。 詳細については、次を参照してください。[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイ](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)します。

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>手順 4:ネットワーク コント ローラー ホスト エージェント サービスを再起動します。
次の Windows PowerShell コマンドを使用すると、ネットワーク コント ローラー ホスト エージェント サービスを再起動します。
    
    Restart-Service nchostagent -Force
    
詳細については、次を参照してください。 [Restart-service](https://technet.microsoft.com/library/hh849823.aspx)します。

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>プロキシの DNS サービスのファイアウォール規則を有効にします。
次の Windows PowerShell コマンドを使用して、VM と、Idn サーバーと通信するプロキシの例外を許可するファイアウォール ルールを作成することができます。
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

詳細については、次を参照してください。 [Enable-netfirewallrule](https://technet.microsoft.com/library/jj554869.aspx)します。
    
### <a name="validate-the-idns-service"></a>Idn サービスを検証します。
Idn サービスを検証するには、サンプル テナント ワークロードをデプロイする必要があります。

詳細については、次を参照してください。 [VM とテナントの仮想ネットワークまたは VLAN への接続を作成](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)です。

テナント VM Idn サービスを使用する場合は、空白のままに、VM ネットワーク インターフェイスの DNS サーバーの構成と DHCP を使用するインターフェイスを許可する必要があります。 

このようなネットワーク インターフェイスを使用して、VM が開始されると後、は、構成、Idn を使用する VM が自動的に受信し、VM がすぐに Idn サービスを使用して名前解決を実行するを開始します。

ネットワーク コント ローラーが、IP アドレスを持つ VM を提供し、Idn サーバーと VM の代わりに DNS 名の登録を実行、テナントのネットワーク インターフェイスの DNS サーバーおよび代替 DNS サーバーの情報は空のままで、Idn サービスを使用する VM を構成する場合. 

ネットワーク コント ローラーは、VM の名前解決を実行するには、VM と、必要な情報についても、Idn プロキシを通知します。 

VM を開始すると、DNS クエリをプロキシは、仮想ネットワークから Idn サービスへのクエリのフォワーダーとして機能します。 

DNS プロキシは、テナント VM のクエリが分離されるも確認します。 Idn サーバー クエリの権限がある場合、Idn サーバーは、権限のある応答を返します。 Idn サーバーにクエリの権限がない場合は、インターネットの名前を解決する DNS 再帰を実行します。

>[!NOTE]
>この情報は、セクションに含める**構成 AttachToVirtualNetwork** SDNExpressTenant.ps1 で。 詳細については、次を参照してください。[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイ](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)します。

