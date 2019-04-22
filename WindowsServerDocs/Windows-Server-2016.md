---
redirect_url: /windows-server/windows-server
ms.openlocfilehash: 6f6e0d21fdf43ce3cf9f713d5731cfea5bb069de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812273"
---
# <a name="windows-server-2016"></a>Windows Server 2016

このライブラリには、IT 担当者が Windows Server 2016 の評価、計画、展開、セキュリティ保護、管理を行うために必要な情報が用意されています。

> [!Note] 
> 次のバージョンの Windows Server は大きく変わります。 Windows Server の新機能の詳細については、「[Windows サーバーの半期チャネルの概要](./get-started/semi-annual-channel-overview.md)」を参照してください。 

[![Windows Server 2016 の概要ビデオ](media/front-page-video.png)](https://www.youtube-nocookie.com/embed/V8oF0JpDzaM)

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/what-s-new-in-windows-server-2016">
        <img height=145 src="media/whats-new-highlight.png" alt="What's new icon" title="Windows Server 2016 の新機能"/></a>
        <br/>新機能
    </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/server-basics">
        <img height=145 src="media/1-getstarted.png" alt="get started icon" title="Windows Server 2016 を使ってみる" /></a>
      <br/>はじめに </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/administration/index">
        <img height=145 src="media/8-management.png" alt="administer icon" title="Windows Server の管理" /></a>
      <br/>管理 </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/failover-clustering/failover-clustering-overview">
        <img height=145 src="media/3-failover.png" alt="Failover clustering icon" title="Windows Server フェールオーバー クラスタリング" /></a>
      <br/>フェールオーバー クラスタリング </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/identity/identity-and-access">
        <img height=145 src="media/4-identity.png" alt="Identity and access icon" title="Windows サーバーの ID およびアクセス" /></a>
      <br>ID およびアクセス </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/networking/networking">
        <img height=145 src="media/6-networking.png" alt="Networking icon" title="Windows Server のネットワーク" />
        </a>
      <br/>ネットワーク </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/remote/index">
        <img height=145 src="media/remote.png" alt="remote icon" title="リモート アクセスおよびサーバー管理" />
        </a>
      <br/>リモート アクセス </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/security/security-and-assurance">
        <img height=145 src="media/5-security.png" alt="Security icon" title="Windows Server のセキュリティおよび保証" />
      </a>
      <br/>セキュリティおよび保証 </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">&nbsp;</td>
    <td align='center' style="width:25%; border:0;"><br>
      <a href="/windows-server/storage/storage">
        <img height=145 src="media/7-storage.png" alt="Storage icon" title="Windows Server 記憶域" />
      </a>
      <br/>ストレージ </td>
   <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/virtualization/virtualization">
        <img height=145 src="media/virtualization.png" alt="virtualization icon" title="Windows Server 仮想化" /></a>
      <br/>仮想化 </td>
    <td align='center' style="width:25%; border:0;">&nbsp; </td>
  </tr>
</table>

<br/>

> [!Note] 
> Windows Server 2016 の新機能を直接確かめたい方は、「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)」で評価版をダウンロードすることができます。 


## <a name="windows-server-2016-editions"></a>Windows Server 2016 の各エディション

Windows Server 2016 のエディションには、Standard、Datacenter、Essentials があります。 Windows Server 2016 Datacenter では、仮想化権限が無制限であることに加えて、ソフトウェアによるデータセンターを構築できる新機能も含まれています。 Windows Server 2016 Standard には、制限付きの仮想化権限とエンタープライズ クラスの機能が備わっています。 Windows Server Essentials は、初めてクラウド接続サーバーを使用する方に最適です。 このエディション向けに[幅広いドキュメント](https://go.microsoft.com/fwlink/?LinkID=827171)が用意されています。ここでは、Standard エディションと Datacenter エディションのみについて説明します。 次の表に、Standard エディションと Datacenter エディションの主要な違いの概要を簡単に示します。

|機能|Datacenter|Standard|  
|-------------------|----------|-----------------------|  
|Windows Server のコア機能| ○| ○|
|OSE/Hyper-V コンテナー|無制限|   2|
|Windows Server コンテナー|無制限|   無制限|
|ホスト ガーディアン サービス| ○| ○|
|Nano Server インストール オプション| ○| ○|
|記憶域スペース ダイレクト、記憶域レプリカなどの記憶域機能| ○| no|
|シールドされた仮想マシン| ○| no|
|ソフトウェアによるネットワーク制御インフラストラクチャ (ネットワーク コントローラー、ソフトウェア ロード バランサー、マルチテナント ゲートウェイ)| ○| no|

詳細については、「[Windows Server 2016 の価格およびライセンス体系](https://www.microsoft.com/en-us/cloud-platform/windows-server-pricing)」および「[Windows Server バージョンの機能の比較](https://www.microsoft.com/en-us/cloud-platform/windows-server-comparison)」を参照してください。

## <a name="installation-options"></a>インストール オプション

Standard エディションおよび Datacenter エディションには、次の 3 つのインストール オプションが用意されています。

- **Server Core:** 必要なディスク領域が抑えられ、攻撃対象領域を減らせると共に、特にサービス要件を緩和できます。 その他のユーザー インターフェイス要素やグラフィカル管理ツールに関するニーズが特にない場合は、このオプションを**お勧めします**。
- **デスクトップ エクスペリエンス搭載サーバー:** Windows Server 2012 R2 では別途インストールする必要があったクライアント エクスペリエンス機能を含め、標準ユーザー インターフェイスとすべてのツールがインストールされます。 サーバー マネージャーまたは他の方法によってサーバーの役割と機能がインストールされます。
- **Nano Server:** プライベート クラウドとデータセンター向けに最適化されたリモート管理サーバー オペレーティング システムです。 Nano Server は Server Core モードの Windows Server に似ていますが、サイズが大幅に小さく、ローカル ログオン機能がありません。さらに、64 ビットのアプリケーション、ツール、およびエージェントのみがサポートされます。 他のオプションと比べて、使用されるディスク領域はかなり小さく、セットアップ時間が大幅に短縮されると共に、必要な更新と再起動の回数がずっと少なくなります。

>[!Note]
> 以前にリリースされた一部の Windows Server とは異なり、インストール後に、Server Core とデスクトップ エクスペリエンス搭載サーバーとの間の変換は実行できません。 たとえば、Server Core をインストールし、後でデスクトップ エクスペリエンス搭載サーバーを使用することになった場合は、新規インストールを実行する必要があります (逆の場合も同様です)


適切なエディションとインストール オプションを確認したら、以下のいずれかをクリックして Windows Server 2016 の使用を開始してください。
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:33%; border:0;">
      <a  href="/windows-server/get-started/getting-started-with-nano-server"> <img width="175" src="media/nano.png" alt="Icon representing Nano server" title="Nano Server - 最も軽量" /><br/>Nano Server - <br/>最も明るい重み</a>
    </td>
    <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-core"> <img width="175" src="media/servercore.png" alt="Icon representing the Server Core installation" title="Server Core - おすすめ" /><br/>Server Core - <br/>お勧めします</a></td>
   <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-with-desktop-experience"><img width="175" src="media/desktop.png" alt="Icon representing the full desktop experience installation option for Windows Server" title="デスクトップ エクスペリエンス - 完全なエクスペリエンス" /><br/>デスクトップ エクスペリエンス - <br/>完全なインターフェイス</a></td>
  </tr>
</table>

## <a name="windows-server-software-defined-datacenter-sddc"></a>Windows Server ソフトウェア定義データ センター (SDDC)

仮想化された記憶域、ネットワーク、セキュリティ、および管理テクノロジは、Windows Server ソフトウェア定義データ センター (SDDC) の構成要素です。
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:10%; border:0;"></td>
    <td align='center' style="width:50%; border:0;"><a href="/windows-server/sddc"><img width="400" src="media/sddc/WS16-heading.png" alt="Icon representing SDDC" title="Windows Server ソフトウェア定義データ センター (SDDC)" /><br/>Windows Server ソフトウェアによるデータ センター (SDDC)</a></td>
    <td align='center' style="width:10%; border:0;"></td>
  </tr>
</table>
