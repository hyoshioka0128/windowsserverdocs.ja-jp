---
title: インストール |アップグレード |Windows Server 2019 への移行します。
description: クリーン インストールをインプレース アップグレードまたは移行する方法は、Windows Server 2019。
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
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810822"
---
# <a name="install--upgrade--migrate-to-windows-server-2019"></a>インストール |アップグレード |Windows Server 2019 への移行します。

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 と Windows Server 2008 の延長サポートは 2020 年 1月で終了します。 [アップグレードのオプションについて説明します](http://aka.ms/upgradecenter)します。

Windows Server の新しいバージョンへ移行する場合、 現在実行しているバージョンに応じて、豊富なオプションを使用できます。

## <a name="clean-install"></a>クリーン インストール
同じハードウェア上で古いバージョンの Windows Server から Windows Server 2019 に移動する場合は、行う必要があります、**クリーン インストール**が古い、同じハードウェア上に直接新しいオペレーティング システムをインストールするだけである場合、したがって、前のオペレーティング システムを削除しています。 これは最も簡単な方法ですが、まずデータをバックアップし、アプリケーションを再インストールする必要があります。 システム要件などの注意してください、これを必ずの詳細を確認するいくつかの事項が[Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124)、 [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558)、 [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)、および[Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)します。

## <a name="in-place-upgrade"></a>インプレース アップグレード

同じハードウェアと、サーバーをフラット化せずに設定するすべてのサーバーの役割を保持する場合は、操作を行いますたい、 **、インプレース アップグレード**古いからすれば、オペレーティング システムを新しいものの設定を維持するサーバーロール、およびデータをそのまま残ります。 たとえば、サーバーで Windows Server 2012 R2 が実行されている場合は、Windows Server 2016 または Windows Server 2019 にアップグレードできます。 ただし、すべての古いオペレーティング システムが、すべての新しいオペレーティング システムに移行できるわけではありません。 使用可能なアップグレード パスの次の図を参照してください。

![Windows Server のインプレース アップグレード パスの図](media/upgrade-paths.png)

アップグレードに関するステップ バイ ステップ ガイダンスについては、次を参照してください、 [Windows Server のアップグレード センター](http://aka.ms/upgradecenter):。

[![Windows Server のアップグレードのセンターのスクリーン ショット](media/upgrade-center.png)](http://aka.ms/upgradecenter)

## <a name="cluster-os-rolling-upgrade"></a>クラスター OS のローリング アップグレード

クラスター OS のローリング アップグレードすると、管理者は、HYPER-V やスケール アウト ファイル サーバーのワークロードを停止することがなく、Windows Server 2012 R2 および Windows Server 2016 からクラスター ノードのオペレーティング システムをアップグレードするができます。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 この新機能の詳細は、「[Cluster operating system rolling upgrade (クラスター オペレーティング システムのローリング アップグレード)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)」で説明されています。

## <a name="migration"></a>Migration

Windows Server の移行は、同じまたは新しいバージョンの Windows Server を実行している別のコンピューターに Windows Server を実行しているソース コンピューターから、一度に 1 つの役割または機能を移動する場合です。 これらのドキュメントで "移行" とは、同じコンピューター上でのアップグレードではなく、役割や機能、データを別のコンピューターに移動することを指します。 

## <a name="license-conversion"></a>ライセンス変換
一部のオペレーティング システム リリースでは、簡単なコマンドと適切なライセンス キーにより、1 回の手順で特定のリリース エディションを同じリリースの別のエディションに変換できます。 これを**ライセンス変換**と呼びます。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。 留意する Server 2016 Datacenter に Server 2016 Standard から移動できる、できない処理をデータ センターから Standard に移動します。 一部の Windows Server のリリースでは、OEM 版、ボリューム ライセンス版、製品版の間を同じコマンドと適切なキーによって自由に変換できます。


 
 
