---
title: Windows Server 2019 のインストール、アップグレード、または移行を行う
description: Windows Server 2019 のクリーン インストール、インプレース アップグレード、または移行を行う方法。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4e99cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 1fd955a640832eb161666f74b93d91bb2c3eff11
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66810822"
---
# <a name="install--upgrade--migrate-to-windows-server-2019"></a>Windows Server 2019 のインストール、アップグレード、または移行を行う

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 と Windows Server 2008 の延長サポートは 2020 年 1月で終了します。 [アップグレードのオプションについて確認してください](http://aka.ms/upgradecenter)。

Windows Server の新しいバージョンへ移行する場合、 現在実行しているバージョンに応じて、豊富なオプションを使用できます。

## <a name="clean-install"></a>クリーン インストール
同じハードウェア上で古いバージョンの Windows Server から Windows Server 2019 に移行する場合は、**クリーン インストール**を行ってください。この方法では、同じハードウェア上の既存のバージョンの上に新しいオペレーティング システムを直接インストールし、これによって既存のオペレーティング システムを削除します。 これは最も簡単な方法ですが、まずデータをバックアップし、アプリケーションを再インストールする必要があります。 システム要件など、いくつか注意すべき点があるため、必ず [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124)、[Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558)、[Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)、[Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) の詳細を確認してください。

## <a name="in-place-upgrade"></a>インプレース アップグレード

同じハードウェアを使い、サーバーをフラット化せずに、セットアップされているすべてのサーバーの役割を保持する場合、**インプレース アップグレード**を行うことがあります。これにより、古いオペレーティング システムから新しいオペレーティング システムに移行し、ユーザーの設定、サーバーの役割、およびデータはそのまま維持されます。 たとえば、サーバーで Windows Server 2012 R2 を実行している場合、Windows Server 2016 または Windows Server 2019 にアップグレードできます。 ただし、すべての古いオペレーティング システムが、すべての新しいオペレーティング システムに移行できるわけではありません。 使用可能なアップグレード パスについては、次の図を参照してください。

![Windows Server のインプレース アップグレード パスの図](media/upgrade-paths.png)

Windows Server のアップグレードに関する手順を追ったガイダンスについては、[Windows Server アップグレード センター](http://aka.ms/upgradecenter)にアクセスしてください。

[![Windows Server アップグレード センターのスクリーンショット](media/upgrade-center.png)](http://aka.ms/upgradecenter)

## <a name="cluster-os-rolling-upgrade"></a>クラスター OS のローリング アップグレード

クラスター OS のローリング アップグレードを使用すると、管理者は、Hyper-V またはスケールアウト ファイル サーバーのワークロードを停止することなく、クラスター ノードのオペレーティング システムを Windows Server 2012 R2 および Windows Server 2016 からアップグレードできます。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 この新機能の詳細は、「[Cluster operating system rolling upgrade (クラスター オペレーティング システムのローリング アップグレード)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)」で説明されています。

## <a name="migration"></a>Migration

Windows Server の移行は、Windows Server を実行する移行元のコンピューターから、同じバージョンまたは新しいバージョンの Windows Server を実行する別の移行先コンピューターに、役割や機能を一度に 1 つずつ移動させることを言います。 これらのドキュメントで "移行" とは、同じコンピューター上でのアップグレードではなく、役割や機能、データを別のコンピューターに移動することを指します。 

## <a name="license-conversion"></a>ライセンス変換
一部のオペレーティング システム リリースでは、簡単なコマンドと適切なライセンス キーにより、1 回の手順で特定のリリース エディションを同じリリースの別のエディションに変換できます。 これを**ライセンス変換**と呼びます。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。 Server 2016 Standard から Server 2016 Datacenter への移行は可能ですが、プロセスを逆にして Datacenter から Standard に移行することはできないことに注意してください。 一部の Windows Server のリリースでは、OEM 版、ボリューム ライセンス版、製品版の間を同じコマンドと適切なキーによって自由に変換できます。


 
 
