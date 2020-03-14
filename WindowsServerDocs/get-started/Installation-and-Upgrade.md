---
title: Windows Server のインストールとアップグレード
description: Windows Server の新しいバージョンをインストール、アップグレード、または移行する方法。
ms.prod: windows-server
ms.date: 05/14/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 98f876bd-63ff-4c3a-95d4-a8dd8d0d119c
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 140f67a9dab5cf1f10cdb0c5c51a031a0dfb9dd3
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323644"
---
# <a name="windows-server-installation-and-upgrade"></a>Windows Server のインストールとアップグレード

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

Windows Server 2019 をお求めですか? [Windows Server 2019 のインストール、アップグレード、または移行](../get-started-19/install-upgrade-migrate-19.md)に関する記事を参照してください。

> [!IMPORTANT]
> Windows Server 2008 R2 と Windows Server 2008 の延長サポートは 2020 年 1月で終了します。 [アップグレードのオプションについて確認してください](#upgrading-from-windows-server-2008-r2-or-windows-server-2008)。

Windows Server の新しいバージョンへ移行する場合、 現在実行しているバージョンに応じて、豊富なオプションを使用できます。

## <a name="installation"></a>インストール

同じハードウェアで Windows Server の新しいバージョンに移動する場合、確実に移行できる方法の 1 つが**クリーン インストール**です。この方法では、同じハードウェア上の既存のバージョンの上に新しいオペレーティング システムを直接インストールし、これによって既存のオペレーティング システムを削除します。 これは最も簡単な方法ですが、まずデータをバックアップし、アプリケーションを再インストールする必要があります。 たとえばシステム要件など、いくつか注意すべき点があるため、必ず [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558)、[Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)、[Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) の詳細を確認してください。

プレリリース版 (Windows Server 2016 Technical Preview など) から製品版 (Windows Server 2016) への移行には、常にクリーン インストールが必要です。

## <a name="migration-recommended-for-windows-server-2016"></a>移行 (Windows Server 2016 への移行で推奨される手順)

Windows Server の移行ドキュメントは、Windows Server を実行する移行元のコンピューターから、同じバージョンまたは新しいバージョンを実行する別の移行先コンピューターに、役割や機能を一度に 1 つずつ移行する場合について記載されています。 これらのドキュメントで "移行" とは、同じコンピューター上でのアップグレードではなく、役割や機能、データを別のコンピューターに移動することを指します。 既存のワークロードやデータを新しいバージョンの Windows Server に移行する場合には、この方法が推奨されます。 移行する場合は、まず Windows Server 向けの[サーバーの役割のアップグレードと移行に関する一覧表](https://go.microsoft.com/fwlink/?LinkId=828595)をご確認ください。

## <a name="cluster-os-rolling-upgrade"></a>クラスター OS のローリング アップグレード
クラスター OS のローリング アップグレードは Windows Server 2016 の新機能です。管理者はこの機能を利用して、Hyper-V やスケールアウト ファイル サーバーのワークロードを停止することなく、クラスター ノードのオペレーティング システムを Windows Server 2012 R2 から Windows Server 2016 にアップグレードできます。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 この新機能の詳細は、「[Cluster operating system rolling upgrade (クラスター オペレーティング システムのローリング アップグレード)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)」で説明されています。

## <a name="license-conversion"></a>ライセンス変換
一部のオペレーティング システム リリースでは、簡単なコマンドと適切なライセンス キーにより、1 回の手順で特定のリリース エディションを同じリリースの別のエディションに変換できます。 これを**ライセンス変換**と呼びます。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。 一部の Windows Server のリリースでは、OEM 版、ボリューム ライセンス版、製品版の間を同じコマンドと適切なキーによって自由に変換できます。

## <a name="upgrade"></a>アップグレード
同じハードウェアを使い、サーバーをフラット化せずに、セットアップされているすべてのサーバーの役割を保持する場合は、**アップグレード**が適切です。これには多くの方法があります。 通常のアップグレードでは、設定、サーバーの役割、データを保持したまま、古いオペレーティング システムから新しいバージョンへと移行します。 たとえば、サーバーが Windows Server 2012 R2 を実行している場合、Windows Server 2016 にアップグレードできます。 ただし、すべての古いオペレーティング システムが、すべての新しいオペレーティング システムに移行できるわけではありません。
 
>[!NOTE]
>仮想マシンでは、アップグレードを正常に実行するために特定の OEM ハードウェア ドライバーが必要とされないため、アップグレードが最も有効です。
 
オペレーティング システムの評価版から製品版、古い製品版から新しい製品版、または場合によってはオペレーティング システムのボリューム ライセンス版から通常の製品版にアップグレードできます。

アップグレードを開始する前に、このページの表で、現在使用しているバージョンやエディションからの移行がサポートされているバージョンやエディションをご確認ください。

Windows Server 2016 Technical Preview で使用できる複数のインストール オプション間の相違点 (各オプションでインストールされる機能や、インストール後に使用できる管理オプションなど) について詳しくは、「[Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828598)」をご覧ください。

>[!NOTE]
>Windows Server のどのバージョンに移行またはアップグレードする場合も、[サポート ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)および対象バージョンのサポート期間を確認し把握したうえで、それに応じて計画を立てる必要があります。 特定の Windows Server リリースのライフサイクルについては、[こちらでご検索ください](https://support.microsoft.com/lifecycle)。
 
 
## <a name="upgrading-to-windows-server-2016"></a>Windows Server 2016 へのアップグレード
アップグレードに関する重要な注意事項と制限事項、Windows Server 2016 のエディション間のライセンス変換、評価版から製品版への変換などについて詳しくは、「[Windows Server 2016 のアップグレード オプションと変換オプション](https://go.microsoft.com/fwlink/?LinkId=828602)」をご覧ください。
 
>[!NOTE]
>注:Server Core インストールからデスクトップ搭載サーバー インストールへの切り替え (およびその逆方向の切り替え) を行うアップグレードはサポートされていません。 アップグレードまたは変換する既存のオペレーティング システムが Server Core インストールである場合は、移行後も新しいオペレーティング システムの Server Core インストールとなります。
 
以下のクイック リファレンス表では、以前の Windows Server 製品版の各エディションから Windows Server 2016 製品版の各エディションへのサポートされているアップグレード オプションを示します。


|使用しているバージョンとエディション:|アップグレード先のバージョンとエディション|
|--------------------------------|---------------------------------------|
|Windows Server 2012 Standard|Windows Server 2016 Standard または Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard または Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Hyper-V Server 2012 R2|Hyper-V Server 2016 (Cluster OS のローリング アップグレード機能を使用)|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 Workgroup|
 
### <a name="license-conversion"></a>ライセンス変換
Windows Server 2016 Standard (製品版) は、Windows Server 2016 Datacenter (製品版) に変換できます。

Windows Server 2016 Essentials (製品版) は、Windows Server 2016 Standard (製品版) に変換できます。

Windows Server 2016 Standard の評価版は、Windows Server 2016 Standard (製品版)、Datacenter (製品版) のいずれかに変換できます。

Windows Server 2016 Datacenter の評価版は、Windows Server 2016 Datacenter (製品版) に変換できます。
 
## <a name="upgrading-to-windows-server-2012-r2"></a>Windows Server 2012 R2 へのアップグレード
アップグレードに関する重要な注意事項と制限事項、Windows Server 2012 R2 のエディション間のライセンス変換、評価版から製品版への変換などについて詳しくは、「[Windows Server 2012 R2 のアップグレード オプション](https://technet.microsoft.com/library/dn303416.aspx)」をご覧ください。

以下のクイック リファレンス表では、以前の Windows Server 製品版の各エディションから Windows Server 2012 R2 製品版の各エディションへのサポートされているアップグレード オプションを示します。

|使用している Windows オペレーティング システム|アップグレード先のエディション|
|-------------------------|---------------------------|
|Windows Server 2008 R2 Datacenter SP1|Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Enterprise SP1|Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Standard SP1|Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter|
|Windows Web Server 2008 R2 SP1|Windows Server 2012 R2 Standard|
|Windows Server 2012 Datacenter|Windows Server 2012 R2 Datacenter|
|Windows Server 2012 Standard|Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter|
|Hyper-V Server 2012|Hyper-V Server 2012 R2|

### <a name="license-conversion"></a>ライセンス変換
Windows Server 2012 Standard (製品版) は、Windows Server 2012 Datacenter (製品版) に変換できます。

Windows Server 2012 Essentials (製品版) は、Windows Server 2012 Standard (製品版) に変換できます。

Windows Server 2012 Standard の評価版は、Windows Server 2012 Standard (製品版)、Datacenter (製品版) のいずれかに変換できます。

## <a name="upgrading-to-windows-server-2012"></a>Windows Server 2012 へのアップグレード
アップグレードに関する重要な注意事項と制限事項、評価版から製品版への変換などについて詳しくは、「[Windows Server 2012 の評価版と更新プログラムのオプション](https://technet.microsoft.com/library/jj574204.aspx)」をご覧ください。
 
以下のクイック リファレンス表では、以前の Windows Server 製品版の各エディションから Windows Server 2012 製品版の各エディションへのサポートされているアップグレード オプションを示します。

|使用している Windows オペレーティング システム|アップグレード先のエディション|
|--------------------------|--------------------------|
|Windows Server 2008 Standard SP2 または Windows Server 2008 Enterprise SP2|Windows Server 2012 Standard、Windows Server 2012 Datacenter|
|Windows Server 2008 Datacenter SP2|Windows Server 2012 Datacenter|
|Windows Web Server 2008|Windows Server 2012 Standard|
|Windows Server 2008 R2 Standard SP1 または Windows Server 2008 R2 Enterprise SP1|Windows Server 2012 Standard、Windows Server 2012 Datacenter|
|Windows Server 2008 R2 Datacenter SP1|Windows Server 2012 Datacenter|
|Windows Web Server 2008 R2|Windows Server 2012 Standard|

### <a name="license-conversion"></a>ライセンス変換
Windows Server 2012 Standard (製品版) は、Windows Server 2012 Datacenter (製品版) に変換できます。

Windows Server 2012 Essentials (製品版) は、Windows Server 2012 Standard (製品版) に変換できます。

Windows Server 2012 Standard の評価版は、Windows Server 2012 Standard (製品版)、Datacenter (製品版) のいずれかに変換できます。

## <a name="upgrading-from-windows-server-2008-r2-or-windows-server-2008"></a>Windows Server 2008 R2 または Windows Server 2008 からのアップグレード

「[Windows Server 2008 と Windows Server 2008 R2 のアップグレード](modernize-windows-server-2008.md)」に記載されているように、Windows Server 2008 R2 および Windows Server 2008 の延長サポートは 2020 年 1 月に終了します。 サポートに空白が生じないようにするには、Windows Server のサポートされているバージョンにアップグレードするか、[特殊な Windows Server 2008 R2 VM](uploading-specialized-WS08-image-to-azure.md) に移行することによって Azure で再ホストする必要があります。 移行およびアップグレードの計画についての情報および考慮事項については、「[Windows Server の移行ガイド](https://go.microsoft.com/fwlink/?linkid=872689)」を確認してください。

オンプレミス サーバーでは、Windows Server 2008 R2 から Windows Server 2016 以降への直接のアップグレード パスはありません。 代わりに、まず Windows Server 2012 R2 にアップグレードし、次に [Windows Server 2016 にアップグレード](#upgrading-to-windows-server-2016)してください。

アップグレードを計画する際は、Windows Server 2012 R2 へのアップグレードの中間の手順として次のガイドラインに注意してください。

  - 32 ビットから 64 ビットのアーキテクチャに、または 1 つのビルドの種類から別のビルドの種類 (fre から chk など) に対してインプレース アップグレードを実行することはできません。

  - インプレース アップグレードは、同じ言語でのみサポートされます。 1 つの言語から別の言語にアップグレードすることはできません。

  - Windows Server 2008 のコア インストールから Windows Server 2012 R2 Server GUI 付き (Windows Server では "フル デスクトップ搭載サーバー" と呼ばれます) に移行することはできません。 アップグレードされたコア インストールをフル デスクトップ搭載サーバーに切り替えることはできますが、Windows Server 2012 R2 でのみ行えます。 Windows Server 2016 以降では、Server Core からフル デスクトップ搭載サーバーへの切り替えがサポート*されない*ため、Windows Server 2016 にアップグレードする前に切り替えを行ってください。
  
詳細については、役割に固有のアップグレードの詳細情報が記載されている、「[Windows Server 2012 の評価版と更新プログラムのオプション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574204\(v=ws.11\))」を参照してください。

