---
title: SDN の internal DNS サービス (iDNS)
description: このトピックでは、Windows Server 2016 でネットワーク定義のソフトウェアと統合されている内部 DNS (Idn) を使用して、ホストされているテナント ワークロードを DNS サービスを提供する方法について説明します。
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
ms.openlocfilehash: 4bdb495b585cf60315dee60f9365e282877fdc1d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="internal-dns-service-idns-for-sdn"></a>SDN の internal DNS サービスの \(iDNS\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

クラウド サービス プロバイダー \(CSP\) または Windows Server 2016 でのソフトウェアがネットワーク定義 \(SDN\) の展開を計画しているエンタープライズ作業している場合は、SDN と統合されている内部 DNS \(iDNS\) を使用して、ホスト型のテナントのワークロードに DNS のサービスを提供できます。

仮想マシンをホスト型 \(VMs\) とアプリケーションは独自のネットワーク内およびインターネット上の外部のリソースと通信するために DNS が必要です。 Idn を提供できますテナント DNS 名前解決サービスでは、ローカルの分離された名前空間とインターネット リソース。

Idn サービス アクセスできないため、テナントの仮想ネットワークから、に以外、Idn プロキシ経由サーバーことはテナントのネットワーク上の悪意のあるアクティビティに対して脆弱になります。

**主な機能**

Idn の主な機能を次に示します。

- 共有の DNS 名前解決サービス テナントのワークロードを提供します。
- 名前解決およびテナント名前空間内の DNS 登録の権限を持つ DNS サービス
- テナントの Vm からインターネット名の解決のための再帰 DNS サービス。
- ファブリックとテナント名の同時ホストを構成するには、必要な場合
- コスト効果の高い DNS ソリューション - テナント必要はありません、独自の DNS インフラストラクチャを展開するには
- Active Directory の統合により、必要な高可用性します。

これらの機能だけでなくインターネット DNS サーバーを開く、AD 統合の状態に保つに関する不安がある場合、境界ネットワーク内の別の再帰的に競合回避モジュールの背後にある Idn サーバーを展開することができます。

Idn はすべての DNS クエリを一元的なサーバーであるため、CSP または Enterprise ことができますもテナント DNS ファイアウォールを実装、フィルターを適用、悪意のあるアクティビティを検出および、一元化された場所でのトランザクションの監査

## <a name="idns-infrastructure"></a>Idn インフラストラクチャ
Idn インフラストラクチャには、Idn サーバーおよび Idn プロキシが含まれます。

### <a name="idns-servers"></a>Idn サーバー
Idn には、VM の DNS リソース レコードなどのテナントに固有のデータをホストする DNS サーバーのセットが含まれています。

Idn サーバーの内部 DNS ゾーンの権限のあるサーバーとパブリック名の競合回避モジュールとしても機能テナントの Vm が外部リソースに接続しようとします。

すべての仮想ネットワーク上のバーチャル マシンのホスト名は、下にある同じゾーンの DNS リソース レコードとして保存されます。 たとえば、contoso.local という名前のゾーンの Idn を展開する場合は、そのネットワーク上のバーチャル マシンの DNS リソース レコードが contoso.local ゾーンに格納されます。

コンピューター名と DNS サフィックスの文字列の GUID 形式で、仮想ネットワークのテナント VM の完全修飾ドメイン名 \(FQDNs\) で構成されます。 たとえば、テナントの仮想ネットワーク contoso, ローカル、上にある TENANT1 という名前の VM がある場合、VM の FQDN は TENANT1 です。*バーチャル ネットワーク guid*. contoso.local]、[場所*バーチャル ネットワーク guid* 、仮想ネットワークの DNS サフィックスの文字列は、します。

>[!NOTE]
>ファブリック管理者の場合は、専用の新しい DNS サーバーを展開するのではなく、Idn サーバーで Idn としてサーバーを使用して、お客様の CSP または企業の DNS インフラストラクチャを使用できます。 Idn の新しいサーバーを展開する場合も、既存のインフラストラクチャを使用して、Idn は高可用性を実現する Active Directory に依存します。 Idn サーバーは、Active Directory と統合するため必要があります。

### <a name="idns-proxy"></a>Idn プロキシ
Idn プロキシは、すべてのホスト上で実行して、テナント Idn サーバーへの仮想ネットワークの DNS トラフィックを転送する Windows サービスです。

次の図は、Idn サーバーに Idn プロキシ経由のテナント仮想ネットワークとインターネットからの DNS トラフィックのパスを示しています。

![Idn インフラストラクチャ](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Idn を展開する方法
スクリプトを使用して Windows Server 2016 SDN を展開するときに、展開では Idn が自動的に含まれます。

詳細については、次のトピックを参照してください。

- [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開します。](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Idn 展開の手順を理解します。
このセクションを使用すると、Idn がインストールされ、SDN のスクリプトを使用してを展開するときに構成する方法を理解します。

Idn の展開に必要な手順の概要を次に示します。

>[!NOTE]
>スクリプトを使用して SDN を展開した場合は、次の手順のいずれかを実行する必要はありません。 情報とトラブルシューティングのみを目的の手順を示します。

### <a name="step-1-deploy-dns"></a>手順 1: DNS を展開します。
次の例の Windows PowerShell コマンドを使用して DNS サーバーを展開することができます。
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>手順 2: ネットワーク コント ローラーで Idn 情報を構成します。
このスクリプトのセグメントは、によって行われた、管理者は、ネットワーク コント ローラーに、Idn ゾーンの構成 -、iDNSServer と Idn 名をホストするために使用するゾーンの IP アドレスなどを知らせる REST 呼び出しです。 

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
>これは、セクションからの抜粋**構成 ConfigureIDns** SDNExpress.ps1 でします。 詳細については、次を参照してください。[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)します。

### <a name="step-3-configure-the-idns-proxy-service"></a>手順 3: Idn プロキシ サービスを構成します。
Idn プロキシ サービスは、各テナントの仮想ネットワークと Idn サーバーが配置されている物理ネットワーク間のブリッジを提供する、HYPER-V ホストで実行します。 すべての HYPER-V ホストで次のレジストリ キーを作成する必要があります。


**DNS ポート:**固定ポート 53

- レジストリ キー HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService ="
- ValueName ="Port"
- セグ = 53
- ValueType ="Dword"
       

**DNS プロキシ ポート:**固定ポート 53

- レジストリ キー HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService ="
- ValueName ="ProxyPort"
- セグ = 53
- ValueType ="Dword"
        
**DNS の ip アドレス:** Idn サービスを使用して、テナントが選択した場合に、ネットワーク インターフェイスに構成されている固定の IP アドレスです。

- レジストリ キー HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService ="
- ValueName ="IP"
- セグ =「169.254.169.254」
- ValueType =「文字列」

        
**Mac アドレス]:** 、DNS サーバーのメディア アクセス制御のアドレス

- レジストリ キー HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService を =
- ValueName ="MAC"
- セグ ="aa-bb-cc-aa-bb-cc"
- ValueType =「文字列」

**サーバーのアドレスを IDN:** Idn サーバーのコンマ区切りリスト。

- レジストリ キー: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- ValueName =「フォワーダ」
- セグ =「10.0.0.9」
- ValueType =「文字列」



>[!NOTE]
>これは、セクションからの抜粋**構成 ConfigureIDnsProxy** SDNExpress.ps1 でします。 詳細については、次を参照してください。[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)します。

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>手順 4: ネットワーク コント ローラー ホスト エージェント サービスを再起動します。
次の Windows PowerShell コマンドを使用すると、ネットワーク コント ローラー ホスト エージェント サービスを再起動します。
    
    Restart-Service nchostagent -Force
    
詳細については、次を参照してください。 [Restart-service](https://technet.microsoft.com/library/hh849823.aspx)します。

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>プロキシの DNS サービスのファイアウォール規則を有効にします。
次の Windows PowerShell コマンドを使用して、VM と、Idn サーバーと通信するプロキシの例外を許可するファイアウォール規則を作成することができます。
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

詳細については、次を参照してください。 [Enable-netfirewallrule](https://technet.microsoft.com/library/jj554869.aspx)します。
    
### <a name="validate-the-idns-service"></a>Idn サービスを検証します。
Idn サービスを検証するには、サンプルのテナント ワークロードを展開する必要があります。

詳細については、次を参照してください。[バーチャル マシンとテナントの仮想ネットワークまたは VLAN に接続を作成する](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)します。

テナント VM Idn サービスを使用する場合は、VM ネットワーク インターフェイスの DNS サーバー構成を空白のままし、DHCP を使用するインターフェイスを許可する必要があります。 

このようなネットワーク インターフェイスを備えた VM が開始した後、Idn を使用する VM を許可する構成が自動的に受信し、Idn サービスを使用して名前解決を実行する VM をすぐに開始します。

テナントの VM ネットワーク インターフェイスの DNS サーバーと代替 DNS サーバーの情報は空のままで、Idn サービスを使用するように構成する場合、ネットワーク コント ローラーは、IP アドレスを持つ VM を提供し、Idn サーバーで VM の代わり DNS 名の登録を実行します。 

また、ネットワーク コント ローラーは、VM の名前解決を実行するには、VM と、必要な情報について、Idn プロキシを通知します。 

VM では、DNS クエリを開始するときに、プロキシは、仮想ネットワークから、Idn サービスへのクエリのフォワーダとして機能します。 

DNS プロキシはまた、テナント VM のクエリが分離されたことを確認します。 Idn サーバー クエリの権限がある場合、Idn サーバーは、権限のある応答を返します。 Idn サーバーが、クエリの権限を持っていない場合は、インターネット名を解決するのには DNS 再帰を実行します。

>[!NOTE]
>セクションでこの情報が含まれている**構成 AttachToVirtualNetwork** SDNExpressTenant.ps1 でします。 詳細については、次を参照してください。[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)します。

