---
title: Windows Server 2019 のインストール、アップグレード、または移行
description: Windows Server のクリーン インストール、インプレース アップグレード、または移行を行う方法
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4e99cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 1c0c6ca10e7ebac16d81fe1393e471a7878fd0ca
ms.sourcegitcommit: ccec91c1d32a978159f9b8bb5e39ead5805c26c4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71143757"
---
# <a name="install-upgrade-or-migrate-to-windows-server"></a>Windows Server のインストール、アップグレード、または移行

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 と Windows Server 2008 の延長サポートは 2020 年 1月で終了します。 [アップグレードのオプションについて確認してください](http://aka.ms/upgradecenter)。 Windows Server 2019 をダウンロードするには、「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)」を参照してください。

Windows Server の新しいバージョンへ移行する場合、 現在実行しているバージョンに応じて、豊富なオプションを使用できます。

## <a name="clean-install"></a>クリーン インストール

Windows Server をインストールする最も簡単な方法は、クリーンインストールを実行することです。この場合、空のサーバーにインストールするか、既存のオペレーティング システムを上書きします。 これは最も簡単な方法ですが、まずデータをバックアップし、アプリケーションを再インストールする必要があります。 システム要件など、いくつか注意すべき点があるため、必ず [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124)、[Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558)、[Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)、[Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) の詳細を確認してください。

## <a name="in-place-upgrade"></a>一括アップグレード

同じハードウェアを使い、サーバーをフラット化せずに、セットアップされているすべてのサーバーの役割を保持する場合、**インプレース アップグレード**を行うことがあります。これにより、古いオペレーティング システムから新しいオペレーティング システムに移行し、ユーザーの設定、サーバーの役割、およびデータはそのまま維持されます。 たとえば、サーバーで Windows Server 2012 R2 を実行している場合、Windows Server 2016 または Windows Server 2019 にアップグレードできます。 ただし、すべての古いオペレーティング システムが、すべての新しいオペレーティング システムに移行できるわけではありません。 

Windows Server のアップグレード手順のガイダンスについては、[Windows Server アップグレード コンテンツ](../upgrade/upgrade-overview.md)をご覧ください。

## <a name="cluster-os-rolling-upgrade"></a>クラスター OS のローリング アップグレード

クラスター OS のローリング アップグレードを使用すると、管理者は、Hyper-V またはスケールアウト ファイル サーバーのワークロードを停止することなく、クラスター ノードのオペレーティング システムを Windows Server 2012 R2 および Windows Server 2016 からアップグレードできます。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 この新機能の詳細は、「[Cluster operating system rolling upgrade (クラスター オペレーティング システムのローリング アップグレード)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)」で説明されています。

## <a name="migration"></a>Migration

Windows Server の移行は、Windows Server を実行する移行元のコンピューターから、同じバージョンまたは新しいバージョンの Windows Server を実行する別の移行先コンピューターに、役割や機能を一度に 1 つずつ移動させることを言います。 これらのドキュメントで "移行" とは、同じコンピューター上でのアップグレードではなく、役割や機能、データを別のコンピューターに移動することを指します。 

## <a name="license-conversion"></a>ライセンス変換

一部のオペレーティング システム リリースでは、簡単なコマンドと適切なライセンス キーにより、1 回の手順で特定のリリース エディションを同じリリースの別のエディションに変換できます。 これを**ライセンス変換**と呼びます。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。 Server 2016 Standard から Server 2016 Datacenter への移行は可能ですが、プロセスを逆にして Datacenter から Standard に移行することはできないことに注意してください。 一部の Windows Server のリリースでは、OEM 版、ボリューム ライセンス版、製品版の間を同じコマンドと適切なキーによって自由に変換できます。