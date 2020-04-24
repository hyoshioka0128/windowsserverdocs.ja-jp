---
title: Windows Server 2016 のアップグレード オプションと変換オプション
description: サポートされているすべての Windows Server 2016 へのアップグレード パスについて説明します。
ms.prod: windows-server
ms.date: 01/18/2017
ms.technology: server-general
ms.topic: article
ms.assetid: 74aa1da3-7076-4a1f-ad5b-9e17bd46dba2
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 05e891d4170458018577b39bc83e952bf18d420e
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826505"
---
# <a name="upgrade-and-conversion-options-for-windows-server-2016"></a>Windows Server 2016 のアップグレード オプションと変換オプション

>適用先:Windows Server 2019、Windows Server 2016

このトピックでは、以前の各種オペレーティング システムから Windows Server&reg; 2016 にアップグレードする場合のさまざまな方法について説明します。

Windows Server 2016 に移るためのプロセスは、開始地点のオペレーティング システムや選択するパスに応じて大きく異なる場合があります。 新しい Windows Server 2016 の展開にかかわる可能性のあるさまざまな操作は次の用語を使用して区別します。

- **インストール** は、基本的な概念としては、ハードウェア上に新しいオペレーティング システムを取得することです。 具体的には、 **クリーン インストール** では以前のオペレーティング システムの削除が必要です。 Windows Server 2016 のインストールについては、[Windows Server 2016 のシステム要件とインストール情報](https://technet.microsoft.com/windows-server-docs/get-started/system-requirements--and-installation)に関するページを参照してください。 他のバージョンの Windows Server のインストールについては、「[Windows Server Installation and Upgrade (Windows Server のインストールとアップグレード)](https://technet.microsoft.com//windowsserver/dn527667)」を参照してください。

- **移行**とは、既存のオペレーティング システムを別のハードウェアや仮想マシンのセットに転送して、そのオペレーティング システムから Windows Server 2016 に移ることを意味します。 移行はインストールしているサーバーの役割に応じて大きく異なる場合があります。移行の詳細については、「[Windows Server Installation, Upgrade, and Migration (Windows Server のインストール、アップグレード、移行)](https://technet.microsoft.com/windowsserver/dn458795)」を参照してください。

- **クラスター OS のローリング アップグレード**は Windows Server 2016 の新機能であり、管理者がこの機能を利用することで、Hyper-V やスケールアウト ファイル サーバーのワークロードを停止することなく、クラスター ノードのオペレーティング システムを Windows Server 2012 R2 から Windows Server 2016 にアップグレードできます。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 この新機能の詳細は、「[Cluster operating system rolling upgrade (クラスター オペレーティング システムのローリング アップグレード)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)」で説明されています。

- 一部のオペレーティング システム リリースの**ライセンス変換**では、簡単なコマンドと適切なライセンス キーにより、1 回の手順でリリースの特定のエディションを同じリリースの別のエディションに変換できます。 これをライセンス変換と呼びます。 たとえば、Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。

- **アップグレード**とは、既存のオペレーティング システム リリースを同じハードウェア上に保持したまま、そのオペレーティング システム リリースからより新しいリリースに移ることです。 (これは、インプレース アップグレードと呼ばれることもあります)。たとえば、サーバーで Windows Server 2012 または Windows Server 2012 R2 を実行している場合、Windows Server 2016 にアップグレードできます。 オペレーティング システムの評価版から製品版、古い製品版から新しい製品版、または場合によってはオペレーティング システムのボリューム ライセンス版から通常の製品版にアップグレードできます。

> [!IMPORTANT]  
> 仮想マシンでは、アップグレードを正常に実行するために特定の OEM ハードウェア ドライバーが必要とされないため、アップグレードが最も有効です。  

> [!IMPORTANT]  
> 14393.0.161119-1705.RS1_REFRESH より前の Windows Server 2016 のリリースでは、Windows Server 2016 を Server Core オプションではなくデスクトップ エクスペリエンス オプションを使用してインストールしている場合にのみ、**このような評価版から製品版への変換を行うことができます**。 バージョン 14393.0.161119-1705.RS1_REFRESH 以降のリリースでは、使ったインストール オプションに関係なく評価版を製品版に移行できます。

> [!IMPORTANT]  
> サーバーで NIC チーミングを使用している場合、アップグレードの前に NIC チーミングを無効にし、アップグレードが完了してから再度有効にします。 詳細については、「[NIC チーミングの概要](https://technet.microsoft.com/library/hh831648(v=ws.11).aspx)」を参照してください。

## <a name="upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016"></a>以前の製品版 Windows Server から Windows Server 2016 へのアップグレード

以下の表は、**既にライセンスを取得している** (つまり評価版でない) Windows オペレーティング システムを Windows Server 2016 のどのエディションにアップグレードできるかを簡単にまとめたものです。

サポートされるパスに関しては、次の一般的なガイドラインがあります。

- 32 ビット アーキテクチャから 64 ビット アーキテクチャへのアップグレードはサポートされていません。 Windows Server 2016 のすべてのエディションが 64 ビット版のみで提供されます。
- 特定の言語から別の言語へのアップグレードはサポートされていません。
- サーバーがドメイン コントローラーの場合は、「[ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする](https://technet.microsoft.com/library/hh994618.aspx)」を参照して重要な情報を確認してください。
- Windows Server 2016 のプレリリース バージョン (プレビュー) からのアップグレードはサポートされていません。 Windows Server 2016 のクリーン インストールを実行してください。
- Server Core インストールからデスクトップ搭載サーバー インストールへの切り替え (およびその逆方向の切り替え) を行うアップグレードはサポートされていません。
- 以前の Windows Server のインストールから Windows Server の評価版へのアップグレードはサポートされていません。 評価版はクリーン インストールでインストールする必要があります。

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


## <a name="per-server-role-considerations-for-upgrading"></a>アップグレード時のサーバーの役割ごとの注意事項

以前の製品版から Windows Server 2016 にアップグレードするためのパスであっても、既にインストールされているサーバーの役割によっては、アップグレード後もこの役割を引き続き機能させるために、追加の準備やアクションが必要になる場合があります。 必要になる追加手順の詳細については、アップグレードする各サーバーの役割について個別の TechNet ライブラリのトピックを参照してください。

## <a name="converting-a-current-evaluation-version-to-a-current-retail-version"></a>現在の評価版から現在の製品版への変換

Windows Server 2016 Standard の評価版を Windows Server 2016 Standard (製品版)、Datacenter (製品版) のいずれかに変換できます。 同様に、Windows Server 2016 Datacenter の評価版を製品版に変換できます。

> [!IMPORTANT]  
> 14393.0.161119-1705.RS1_REFRESH より前の Windows Server 2016 のリリースでは、Windows Server 2016 を Server Core オプションではなくデスクトップ エクスペリエンス オプションを使用してインストールしている場合にのみ、このような評価版から製品版への変換を行うことができます。 バージョン 14393.0.161119-1705.RS1_REFRESH 以降のリリースでは、使ったインストール オプションに関係なく評価版を製品版に移行できます。

評価版から製品版に乗り換える前に、実際に評価版が実行されていることをご確認ください。 これを行うには、次のいずれかの操作を行います。

- 管理者特権でのコマンド プロンプトで **slmgr.vbs /dlv** を実行します。評価版の場合は、出力に EVAL と表示されます。

- スタート画面で、 **[コントロール パネル]** を開きます。 **[システムとセキュリティ]** を開き、 **[システム]** を開きます。 **[システム]** ページの Windows のライセンス認証の領域に Windows のライセンス認証の状態が表示されます。 **[Windows ライセンス認証の詳細を表示]** をクリックすると、Windows のライセンス認証の状態に関する詳しい情報が表示されます。

既に Windows のライセンス認証が済んでいる場合は、デスクトップに評価期間の残りの期間が表示されます。

サーバー上で評価版ではなく製品版が実行されている場合は、Windows Server 2016 へのアップグレード方法について、このトピックの「以前の製品版 Windows Server から Windows Server 2016 へのアップグレード」セクションを参照してください。

**Windows Server 2016 Essentials の場合**:**slmgr.vbs** コマンドに販売キー、ボリューム ライセンス キー、または OEM キーを入力することで、完全製品版に変換できます。

サーバーで Windows Server 2016 Standard または Windows Server 2016 Datacenter の評価版を実行している場合は、次の手順に従って製品版に変換できます。

1.    サーバーが**ドメイン コントローラー**の場合は、製品版には変換できません。 この場合は、まず製品版を実行するサーバーに追加のドメイン コントローラーをインストールし、評価版で実行されているドメイン コントローラーから AD DS を削除します。 詳細については、「[ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする](https://technet.microsoft.com/library/hh994618.aspx)」を参照してください。
2.    ライセンス条項を読みます。
3.    管理者特権でのコマンド プロンプトで、 **DISM /online /Get-CurrentEdition**コマンドを実行して現在のエディション名を確認します。 エディション名の簡略形式であるエディション ID をメモしておきます。 次に、エディション ID と販売プロダクト キーを指定して、**DISM /online /Set-Edition:\<エディション ID\> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula** を実行します。 サーバーが 2 回再起動します。

Windows Server 2016 Standard の評価版の場合は、同じコマンドと該当するプロダクト キーを使用して、1 回の操作で Windows Server 2016 Datacenter の製品版に変換することもできます。

> [!TIP] 
> Dism.exe について詳しくは、「[DISM コマンド ライン オプション](https://go.microsoft.com/fwlink/?LinkId=192466)」をご覧ください。

## <a name="converting-a-current-retail-edition-to-a-different-current-retail-edition"></a>現在の製品版から異なる現在の製品版への変換

Windows Server 2016 をインストールした後であればいつでも、セットアップを実行してインストールを修復 (修復セットアップとも呼ばれます) したり、場合によっては別のエディションに変換できます。
セットアップを実行して、任意のエディションの Windows Server 2016 で修復セットアップを実行することができます。これにより、開始時と同じエディションになります。

Windows Server 2016 Standard では、以下に従って、Windows Server 2016 Datacenter に変換できます。管理者特権でのコマンド プロンプトで、 **DISM /online /Get-CurrentEdition**コマンドを実行して現在のエディション名を確認します。 Windows Server 2016 Standard の場合、これは `ServerStandard` になります。 **DISM/online/Get-TargetEditions** コマンドを実行して、アップグレードできるエディションの ID を取得します。 このエディション ID (エディション名の簡略形式) をメモしておきます。 次に、ターゲットのエディション ID と販売プロダクト キーを指定して、**DISM /online /Set-Edition:\<エディション ID\> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula** を実行します。 サーバーが 2 回再起動します。

## <a name="converting-a-current-retail-version-to-a-current-volume-licensed-version"></a>現在の製品版から現在のボリューム ライセンス版への変換

Windows Server 2016 をインストールした後、いつでも自由に製品版、ボリューム ライセンス版、または OEM 版の間で変換を行うことができます。 この変換の間は、同じエディションが維持されます。 変換元が評価版である場合は、最初に評価版を製品版に変換します。その後で、ここで説明されている相互変換を実行することができます。

変換を行うには、管理者特権でのコマンド プロンプトから、**slmgr /ipk \<key\>** を実行します。

\<key\> は、適切なボリューム ライセンス、製品、または OEM のプロダクト キーです。
