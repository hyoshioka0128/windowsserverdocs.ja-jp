---
title: デスクトップ エクスペリエンス搭載サーバーのインストール
description: 'デスクトップ エクスペリエンス搭載サーバー インストールを入手してインストールする方法について説明します。 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 01/18/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b38b8a0-4dfc-4130-be00-fc58bba99595
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 2d92ae9e0013d622c1e0a6b8b6a1662dc82360f2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391789"
---
# <a name="install-server-with-desktop-experience"></a>デスクトップ エクスペリエンス搭載サーバーのインストール
> 適用先:Windows Server 2016
  

Windows Server 2016 をセットアップ ウィザードを使用してインストールするときは、**Windows Server 2016** と **Windows Server (デスクトップ エクスペリエンス搭載サーバー)** のどちらかを選択できます。 Windows Server 2016 のデスクトップ エクスペリエンス搭載サーバー オプションは、Windows Server 2012 R2 で利用できるフル インストール オプションにデスクトップ エクスペリエンス機能のインストールを加えたものに相当します。 セットアップ ウィザードでこの選択をしない場合、**Windows Server 2016** がインストールされます。これが **Server Core** インストール オプションです。

デスクトップ エクスペリエンス搭載サーバー オプションを選択すると、Windows Server 2012 R2 では別途インストールが必要だったクライアント エクスペリエンス機能を含め、標準のユーザー インターフェイスとツールがすべてインストールされます。 サーバー マネージャーまたは他の方法によってサーバーの役割と機能がインストールされます。 Server Core オプションと比較した場合、より多くのディスク領域が必要となるほか、サービスの要件が厳しくなります。したがって、デスクトップ エクスペリエンス搭載サーバー オプションに含まれている追加的なユーザー インターフェイス要素やグラフィカル管理ツールを特に必要としなければ、Server Core インストールを選択することをお勧めします。 追加の要素を使用せずに作業できると判断した場合は、[Install Server Core](Getting-Started-with-Server-Core.md) (Server Core のインストール) を参照してください。 さらに軽量なオプションについては、「[Install Nano Server](Getting-Started-with-Nano-Server.md)」 (Nano Server のインストール) を参照してください。

> [!NOTE]
>
> 以前にリリースされた一部の Windows Server とは異なり、インストール後に、Server Core とデスクトップ エクスペリエンス搭載サーバーとの間の変換は実行できません。 デスクトップ エクスペリエンス搭載サーバーをインストールし、後で Server Core を使用することになった場合は、新規インストールを実行する必要があります。

**ユーザー インターフェイス:** 標準のグラフィカル ユーザー インターフェイス ("サーバー グラフィック シェル")。 サーバー グラフィック シェルには、Windows 10 の新しいシェルが含まれています。 このオプションによって既定でインストールされる具体的な Windows 機能は、User-Interfaces-Infra、Server-GUI-Shell、Server-GUI-Mgmt-Infra、InkAndHandwritingServices、ServerMediaFoundation、およびデスクトップ エクスペリエンスです。 これらの機能は、このリリースのサーバー マネージャーに表示されますが、アンインストールはサポートされておらず、今後のリリースでは入手できません。

**サーバーの役割をローカルにインストール、構成、アンインストール:** サーバー マネージャーまたは Windows PowerShell を使用

**サーバーの役割をリモートでインストール、構成、アンインストール:** サーバー マネージャー、リモート サーバー、RSAT、または Windows PowerShell を使用

**Microsoft 管理コンソール: インストール済み**

## <a name="installation-scenarios"></a>インストールのシナリオ

### <a name="evaluation"></a>評価
「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)」で 180 日間ライセンスが有効な Windows Server の評価版を入手できます。 **[Windows Server 2016 | 64-bit ISO option (Windows Server 2016 | 64 ビット ISO オプション)]** を選択してダウンロードするか、**Windows Server 2016 の仮想ラボ**のページにアクセスします。

> [!IMPORTANT]  
> 14393.0.161119-1705.RS1_REFRESH より前の Windows Server 2016 のリリースでは、Windows Server 2016 を Server Core オプションではなくデスクトップ エクスペリエンス オプションを使用してインストールしている場合にのみ、このような評価版から製品版への変換を行うことができます。 バージョン 14393.0.161119-1705.RS1_REFRESH 以降のリリースでは、使ったインストール オプションに関係なく評価版を製品版に移行できます。


### <a name="clean-installation"></a>クリーン インストール

デスクトップ エクスペリエンス搭載サーバー インストール オプションで Windows Server をインストールするには、ドライブにメディアを挿入し、コンピューターを再起動して、Setup.exe を実行します。 表示されるウィザードで **Windows Server (デスクトップ エクスペリエンス搭載サーバー)** (Standard または Datacenter) を選択して、ウィザードを完了します。

### <a name="upgrade"></a>アップグレード パッケージ、アップグレード
**アップグレード**とは、既存のオペレーティング システム リリースを同じハードウェア上に保持したまま、そのオペレーティング システム リリースからより新しいリリースに移ることです。

適切な Windows Server 製品のフル インストールを既に持っている場合は、以下に示すように、Windows Server 2016 の適切なエディションのデスクトップ エクスペリエンス搭載サーバー インストールにアップグレードできます。

> [!IMPORTANT]  
> このリリースでは、アップグレードは、アップグレードを正常に実行するために特定の OEM ハードウェア ドライバーが必要ない仮想マシンにおいて、最も有効です。 それ以外の場合は、移行が推奨されます。  

- 32 ビット アーキテクチャから 64 ビット アーキテクチャへの一括アップグレードはサポートされません。 Windows Server 2016 のすべてのエディションが 64 ビット版のみで提供されます。
- 1 つの言語から別の言語への一括アップグレードはサポートされません。
- サーバーがドメイン コントローラーの場合は、「[ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする](https://technet.microsoft.com/library/hh994618.aspx)」を参照して重要な情報を確認してください。
- Windows Server 2016 のプレリリース バージョン (プレビュー) からのアップグレードはサポートされていません。 Windows Server 2016 のクリーン インストールを実行してください。
- Server Core インストールからデスクトップ搭載サーバー インストールへの切り替え (およびその逆方向の切り替え) を行うアップグレードはサポートされていません。

左の列に現在使用しているバージョンが見つからない場合、このリリースの Windows Server 2016 へのアップグレードはサポートされません。

右の列に複数のエディションが記載されている場合、同じ開始バージョンから**いずれかの**エディションにアップグレードできます。

|使用しているエディション|アップグレード先のエディション|  
|-------------------|----------|  
|Windows Server 2012 Standard|Windows Server 2016 Standard または Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard または Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 Workgroup|

ボリューム ライセンス版や評価版などの間でのライセンスの変換など、Windows Server 2016 に移るためのさまざまな追加オプションの詳細については、[アップグレード オプション](Supported-Upgrade-Paths.md)に関するページを参照してください。

### <a name="migration"></a>Migration
**移行**とは、ハードウェアまたは仮想マシンの異なるセットにクリーン インストールを実行した後、古いサーバーのワークロードを新しいサーバーに転送することによって既存のオペレーティング システムから Windows Server 2016 に移ることを表します。 移行はインストールしているサーバーの役割に応じて大きく異なる場合があります。移行の詳細については、「[Windows Server Installation, Upgrade, and Migration (Windows Server のインストール、アップグレード、移行)](https://technet.microsoft.com/windowsserver/dn458795)」を参照してください。

移行できるかどうかは、サーバーの役割によって異なります。 次の表には、特に Windows Server 2016 に移る際のサーバーの役割のアップグレードおよび移行オプションの説明が示されています。 個々の役割の移行ガイドについては、「[Windows Server の役割と機能を移行する](https://technet.microsoft.com/windowsserver/jj554790.aspx)」を参照してください。 インストールとアップグレードの詳細については、「[Windows Server Installation, Upgrade, and Migration (Windows Server のインストール、アップグレード、移行)](https://technet.microsoft.com/windowsserver/dn458795)」を参照してください。

|サーバーの役割|Windows Server 2012 R2 からアップグレードできるか?|Windows Server 2012 からアップグレードできるか?|移行はサポートされているか?|ダウンタイムなしで移行を完了できるか?|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory 証明書サービス| 〇|    〇|    〇|    X|
|Active Directory Domain Services|  〇|    〇|    〇|    〇|
|Active Directory フェデレーション サービス|  X| X| 〇|    いいえ (新しいノードをファームに追加する必要がある)|
|Active Directory ライトウェイト ディレクトリ サービス|   〇|    〇|    〇|    〇|
|Active Directory Rights Management サービス|   〇|    〇|    〇|    X|
|フェールオーバー クラスター|はい (ノードの一時停止、ドレイン、削除、Windows Server 2016 へのアップグレード、元のクラスターへの再参加を含む[クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) プロセスを使用)。 はい (アップグレードのためにサーバーがクラスターによって削除された後、別のクラスターに追加された場合)。|いいえ (サーバーがクラスターに属している場合)。 はい (アップグレードのためにサーバーがクラスターによって削除された後、別のクラスターに追加された場合)。  |〇|いいえ (Windows Server 2012 フェールオーバー クラスターの場合)。 はい (Hyper-V VM を備えた Windows Server 2012 R2 フェールオーバー クラスター、またはスケールアウト ファイル サーバーの役割を実行している Windows Server 2012 R2 フェールオーバー クラスターの場合)。 [クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)に関するページを参照。|
|ファイル サービスおよび記憶域サービス| 〇|    〇|    サブ機能によって異なる|  X|
|印刷サービスと FAX サービス|    X| X| はい (Printbrm.exe)| X|
|リモート デスクトップ サービス|   はい (すべてのサブロールで可能。ただし、混在モードのファームはサポートされていない)|   はい (すべてのサブロールで可能。ただし、混在モードのファームはサポートされていない)|   〇|    X|
|Web サーバー (IIS)|  〇|    〇|    〇|    X|
|Windows Server Essentials Experience|  〇|    該当なし - 新機能|  〇|    X|
|Windows Server Update Services|    〇|    〇|    〇|    X|
|ワーク フォルダー|  〇|    〇|    〇|    はい ([クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)を使用した場合に WS 2012 R2 クラスターから)。|

> [!IMPORTANT]  
> セットアップが完了し、必要なサーバーの役割と機能をすべてインストールしたら、Windows Update またはその他の更新方法を使用して Windows Server 2016 に適用可能な更新プログラムがあるかどうかをすぐに確認し、ある場合はインストールします。

---------------------------------------
別のインストール オプションが必要な場合、またはインストールを完了して特定のワークロードを展開する準備が整っている場合は、[Windows Server 2016 のメイン ページ](Windows-Server-2016.md)に戻ってください。