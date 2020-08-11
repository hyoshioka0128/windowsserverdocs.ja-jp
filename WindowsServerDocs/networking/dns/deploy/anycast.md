---
title: エニーキャスト DNS の概要
description: このトピックでは、エニーキャスト DNS の概要について説明します。
manager: laurawi
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: greglin
author: greg-lindsay
ms.openlocfilehash: 2f91ace398cf236967fadde21db7ea0957640995
ms.sourcegitcommit: c4f30b1617571fe434c7fe054695d163e73506b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048900"
---
# <a name="anycast-dns-overview"></a>エニーキャスト DNS の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2019

このトピックでは、エニーキャスト DNS のしくみについて説明します。

## <a name="what-is-anycast"></a>エニーキャストとは

エニーキャストは、それぞれが同じ IP アドレスを割り当てられたエンドポイントのグループに複数のルーティングパスを提供するテクノロジです。 グループ内の各デバイスは、ネットワーク上で同じアドレスをアドバタイズし、ルーティングプロトコルを使用して最適な宛先を選択します。

エニーキャストを使用すると、DNS や HTTP などのステートレスサービスを、同じ IP アドレスの背後に複数のノードを配置し、同等コストのマルチパス (ECMP) ルーティングを使用して、これらのノード間でトラフィックを送信することで、拡張できます。 エニーキャストはユニキャストとは異なり、各エンドポイントには独自の個別の IP アドレスがあります。 

## <a name="why-use-anycast-with-dns"></a>DNS でエニーキャストを使用する理由

エニーキャスト DNS を使用すると、dns サーバーまたはサーバーのグループを有効にして、dns クライアントの地理的な場所に基づいて DNS クエリに応答できます。 これにより、DNS の応答時間が短縮され、DNS クライアントの設定が簡素化されます。 また、エニーキャスト DNS は追加の冗長性レイヤーを提供し、DNS サービス拒否攻撃から保護するのに役立ちます。 

### <a name="how-anycast-dns-works"></a>エニーキャスト DNS のしくみ

エニーキャスト DNS は、Border Gateway Protocol (BGP) などのルーティングプロトコルを使用して dns クエリを優先 DNS サーバーまたは DNS サーバーのグループ (たとえば、ロードバランサーによって管理される DNS サーバーのグループ) に送信します。 これにより、クライアントに最も近い dns サーバーから DNS 応答を取得することで、DNS 通信を最適化できます。

エニーキャストを使用すると、複数の地理的な場所に存在するサーバーはそれぞれ、単一の同一の IP アドレスをローカルゲートウェイ (ルーター) に提供します。 DNS クライアントがエニーキャストアドレスへのクエリを開始すると、利用可能なルートが評価され、DNS クエリが優先する場所に送信されます。 一般に、これはネットワークトポロジに基づく最も近い場所です。 次の例を参照してください。

![エニーキャスト DNS](../../media/Anycast/anycast.png)

**図 1**: ネットワーク上の異なるサイトに配置されている4つの DNS サーバーが、ネットワークに対して同じエニーキャスト IP アドレス (黒い矢印) をアナウンスします。 DNS クライアントデバイスは、エニーキャスト IP アドレスに要求を送信します。 ネットワークデバイスは、使用可能なルートを分析し、クライアントの DNS クエリを最も近い場所 (青い矢印) に送信します。 

現在、エニーキャスト DNS は、多くのグローバル DNS サービスの DNS トラフィックをルーティングするために使用されます。 たとえば、ルート DNS サーバーシステムは、エニーキャスト DNS に大きく依存します。 また、エニーキャストはさまざまなルーティングプロトコルで動作し、イントラネット上でのみ使用できます。

## <a name="windows-server-native-bgp-anycast-demo"></a>Windows Server ネイティブ BGP エニーキャストデモ

次の手順では、Windows Server 上のネイティブ BGP をエニーキャスト DNS と共に使用する方法について説明します。  

### <a name="requirements"></a>必要条件

- Hyper-v の役割がインストールされている1台の物理デバイス。
  - Windows Server 2012 R2、Windows 10 以降。
- 2つのクライアント Vm (任意のオペレーティングシステム)。
  - 詳細については、「発掘」などの BIND ツールをインストールすることをお勧めします。
- 3サーバー Vm (Windows Server 2016 または Windows Server 2019)。
  - Windows PowerShell LoopbackAdapter モジュールがサーバー Vm (DC001、DC002) にまだインストールされていない場合は、このモジュールをインストールするためにインターネットアクセスが一時的に必要になります。

### <a name="hyper-v-setup"></a>Hyper-v のセットアップ

次のように、Hyper-v サーバーを構成します。

- 2プライベート仮想スイッチネットワークが構成されています
  - モックインターネットネットワーク 131.253.1.0/24
  - モックイントラネットネットワーク 10.10.10.0/24
- 2クライアント Vm は 131.253.1.0/24 ネットワークに接続されています
- 2サーバー Vm は 10.10.10.0/24 ネットワークに接続されています
- 1台のサーバーはデュアルホームで、131.253.1.0/24 ネットワークと 10.10.10.0/24 ネットワークの両方に接続されています。

### <a name="virtual-machine-network-configuration"></a>仮想マシンのネットワーク構成

次の設定を使用して、仮想マシンのネットワーク設定を構成します。

1.  Client1、全方法
  - Client1: 131.253.1.1
  - 131.253.1.2:
  - サブネット マスク: 255.255.255.0
  - DNS: 51.51.51.51
  - ゲートウェイ: 131.253.1.254
2.  ゲートウェイ (Windows Server)
  - NIC1: 131.253.1.254、サブネット255.255.255.0
  - NIC2: 10.10.10.254、サブネット255.255.255.0
  - DNS: 51.51.51.51
  - ゲートウェイ: 131.253.1.100 (デモでは無視できます)
3.  DC001 (Windows Server)
  - NIC1: 10.10.10.1 が
  - サブネット: 255.255.255.0
  - DNS: 10.10.10.1 が
4.  DC002 (Windows Server)
  - NIC1: 10.10.10.2
  - サブネット255.255.255.0
  - DNS: 10.10.10.2

### <a name="configure-dns"></a>DNS を構成する

サーバーマネージャーと DNS 管理コンソールまたは Windows PowerShell を使用して、次のサーバーの役割をインストールし、2つのサーバーのそれぞれに静的 DNS ゾーンを作成します。

1.  DC001, DC002
  - Active Directory Domain Services をインストールし、ドメインコントローラーに昇格する (省略可能)
  - DNS ロールをインストールする (必須)
  - DC001 と DC002 の両方で、tst.bvt という名前の静的ゾーン (非 AD 統合) を作成し**ます。**
    - "TXT" タイプのゾーンに単一の静的レコードネーム**サーバー**を追加します。
    - DC001 の TXT レコードのデータ (テキスト) = **DC001**
    - DC002 の TXT レコードのデータ (テキスト) = **DC002**

### <a name="configure-loopback-adapters"></a>ループバックアダプターを構成する

DC001 と DC002 の管理者特権の Windows PowerShell プロンプトで次のコマンドを入力して、ループバックアダプターを構成します。 

> [!NOTE]
> **モジュールのインストール**コマンドにはインターネットアクセスが必要です。 これを行うには、Hyper-v の外部ネットワークに VM を一時的に割り当てます。

```PowerShell
$primary_interface = (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
$loopback_ipv4 = '51.51.51.51'
$loopback_ipv4_length = '32'
$loopback_name = 'Loopback'
Install-Module -Name LoopbackAdapter -MinimumVersion 1.2.0.0 -Force
Import-Module -Name LoopbackAdapter
New-LoopbackAdapter -Name $loopback_name -Force
$interface_loopback = Get-NetAdapter -Name $loopback_name
$interface_main = Get-NetAdapter -Name $primary_interface
Set-NetIPInterface -InterfaceIndex $interface_loopback.ifIndex -InterfaceMetric "254" -WeakHostReceive Enabled -WeakHostSend Enabled -DHCP Disabled
Set-NetIPInterface -InterfaceIndex $interface_main.ifIndex -WeakHostReceive Enabled -WeakHostSend Enabled
Set-NetIPAddress -InterfaceIndex $interface_loopback.ifIndex -SkipAsSource $True
Get-NetAdapter $loopback_name | Set-DNSClient –RegisterThisConnectionsAddress $False
New-NetIPAddress -InterfaceAlias $loopback_name -IPAddress $loopback_ipv4 -PrefixLength $loopback_ipv4_length -AddressFamily ipv4
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_msclient
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_pacer
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_server
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_lltdio
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_rspndr
```

### <a name="virtual-machine-routing-configuration"></a>バーチャルマシンルーティングの構成

Vm で次の Windows PowerShell コマンドを使用して、ルーティングを構成します。

1.  Gateway
```PowerShell
Install-RemoteAccess -VpnType RoutingOnly
Add-BgpRouter -BgpIdentifier “10.10.10.254” -LocalASN 8075
```

2.  DC001
```PowerShell
Install-RemoteAccess -VpnType RoutingOnly
Add-BgpRouter -BgpIdentifier “10.10.10.1” -LocalASN 65511
Add-BgpPeer -Name "Labgw" -LocalIPAddress 10.10.10.1 -PeerIPAddress 10.10.10.254 -PeerASN 8075 –LocalASN 65511
Add-BgpCustomRoute -Network 51.51.51.0/24
```

3.  DC002
```PowerShell
Install-RemoteAccess -VpnType RoutingOnly
Add-BgpRouter -BgpIdentifier "10.10.10.2" -LocalASN 65511
Add-BgpPeer -Name "Labgw" -LocalIPAddress 10.10.10.2 -PeerIPAddress 10.10.10.254 -PeerASN 8075 –LocalASN 65511
Add-BgpCustomRoute -Network 51.51.51.0/24
```

### <a name="summary-diagram"></a>概要図

![エニーキャスト DNS](../../media/Anycast/anycast-lab.png)

**図 2**: ネイティブ BGP エニーキャスト DNS デモ用のラボセットアップ

## <a name="anycast-dns-demonstration"></a>エニーキャスト DNS のデモンストレーション


1.  ゲートウェイサーバーで BGP ルーティングを確認する

    PS C: \> BgpRouteInformation

    DestinationNetwork NextHop LearnedFromPeer State LocalPref MED<br>
    ------------------ -------    --------------- ----- --------- ---<br>
    51.51.51.0/24 10.10.10.1 が DC001 Best<br>
    51.51.51.0/24 10.10.10.2 DC002 Best<br>

2.  Client1 と51.51.51.51 の場合は、

    PS C: \> ping 51.51.51.51

    32バイトのデータを使用して51.51.51.51 に ping を実行します。<br>
    Reply from 51.51.51.51: bytes = 32 time<1 ミリ秒 TTL = 126<br>
    Reply from 51.51.51.51: bytes = 32 time<1 ミリ秒 TTL = 126<br>
    Reply from 51.51.51.51: bytes = 32 time<1 ミリ秒 TTL = 126<br>
    Reply from 51.51.51.51: bytes = 32 time<1 ミリ秒 TTL = 126

    51.51.51.51 の Ping 統計:<br>
    パケット: 送信 = 4、受信 = 4、損失 = 0 (0% 損失)、<br>
    おおよそのラウンドトリップ時間 (ミリ秒):<br>
    最小 = 0ms、Maximum = 0ms、Average = 0ms

3.  Client1 との場合は、nslookup または掘り下げを使用して TXT レコードのクエリを実行します。 両方の例を次に示します。

    PS C: \> TST.BVT TXT + short を掘り下げます。<br>
    PS C: \> nslookup-type = txt tst.bvt 51.51.51.51

    1つのクライアントに "DC001" と表示され、もう一方のクライアントは "DC002" を表示して、エニーキャストが正常に機能していることを確認します。  ゲートウェイサーバーからクエリを実行することもできます。

4.  次に、DC001 でイーサネットアダプターを無効にします。

    PS C: \> (Get NetAdapter)。指定<br>
    ループバック<br>
    イーサネット2<br>
    PS C: \> -NetAdapter "イーサネット 2" を無効にします。<br>
    Confirm<br>
    この操作を実行しますか?<br>
    無効-NetAdapter ' イーサネット 2 '<br>
    [Y] Yes [A] Yes to All [N] No [L] No All [S] Suspend [?]ヘルプ (既定値は "Y"):<br>
    PS C: \> (Get NetAdapter)。オンライン<br>
    上へ<br>
    無効

5.  以前に DC001 から応答を受信していた DNS クライアントが DC002 に切り替えたことを確認します。

    PS C: \> nslookup-type = txt tst.bvt 51.51.51.51<br>
    サーバー: 不明<br>
    アドレス: 51.51.51.51<br>

    tst.bvt text =

    "DC001"<br>
    PS C: \> nslookup-type = txt tst.bvt 51.51.51.51<br>
    サーバー: 不明<br>
    アドレス: 51.51.51.51<br>

    tst.bvt text =

    "DC002"

6.  ゲートウェイサーバーで Get-bgpstatistics を使用して、DC001 で BGP セッションが停止していることを確認します。
7.  DC001 でもう一度イーサネットアダプターを有効にし、BGP セッションが復元されたことを確認し、クライアントが DC001 から再び DNS 応答を受信することを確認します。

> [!NOTE]
> ロードバランサーが使用されていない場合、使用可能な場合は、個々のクライアントが同じバックエンド DNS サーバーを使用します。 これにより、クライアントの一貫性のある BGP パスが作成されます。 詳細については、「4.4.3 of RFC4786: [Equal Cost Paths](https://tools.ietf.org/html/rfc4786#page-10)」セクションを参照してください。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

Q: エニーキャスト DNS はオンプレミスの DNS 環境で使用するのに適したソリューションですか。<br>
A: エニーキャスト DNS は、オンプレミスの DNS サービスとシームレスに連携します。 ただし、DNS サービスの規模を変更するには、エニーキャストは*必要*ありません。
 
Q: ドメインコントローラーの数が多い (例: >50) 環境にエニーキャスト DNS を実装すると、どのような影響がありますか。 <br>
A: 機能に直接的な影響はありません。 ロードバランサーを使用する場合は、ドメインコントローラーに追加の構成は必要ありません。
 
Q: Microsoft カスタマーサービスでサポートされているエニーキャスト DNS 構成はありますか。<br>
A: Microsoft 以外のロードバランサーを使用して DNS クエリを転送する場合、Microsoft は、DNS サーバーサービスに関連する問題をサポートします。 DNS 転送に関連する問題については、ロードバランサーのベンダーに問い合わせてください。 
 
Q: ドメインコントローラーの数が多い (例: >50) ことのあるエニーキャスト DNS のベストプラクティスは何ですか。<br>
A: 各地理的な場所でロードバランサーを使用することをお勧めします。 ロードバランサーは、通常、外部ベンダーによって提供されます。 

Q: エニーキャスト DNS と Azure DNS 同様の機能がありますか。<br>
A: Azure DNS はエニーキャストを使用します。 Azure DNS でエニーキャストを使用するには、Azure DNS サーバーに要求を転送するようにロードバランサーを構成します。 