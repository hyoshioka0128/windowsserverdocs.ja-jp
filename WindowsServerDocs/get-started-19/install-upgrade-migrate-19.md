---
title: インストール |アップグレード |Windows Server 2019 への移行します。
description: クリーン インストール、インプレース アップグレードまたは Windows Server 2019 へ移行する方法。
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
ms.openlocfilehash: 58c363fc0a1e336519bc6ec4276651345cc2b5eb
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121391"
---
# インストール |アップグレード |Windows Server 2019 への移行します。

>適用対象: Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 と Windows Server 2008 の延長サポートは 2020 年 1月で終了します。 [アップグレード オプションについて説明します](http://aka.ms/upgradecenter)。

Windows Server の新しいバージョンへ移行する場合、 現在実行しているバージョンに応じて、豊富なオプションを使用できます。

## インストールをクリーンアップします。
同じハードウェア上の Windows Server 2019 を Windows Server の以前のバージョンから移行する場合は、**クリーン インストール**、削除するため、同じハードウェア上に直接新しいオペレーティング システムをインストールするを行う必要があります、以前のオペレーティング システム。 これは最も簡単な方法ですが、まずデータをバックアップし、アプリケーションを再インストールする必要があります。 すべき、システム要件など、 [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124)、 [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558)、 [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)、および[Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)の詳細を確認することを確認するために、いくつかのことがあります。

## 一括アップグレード
同じハードウェアと、サーバーをフラット化せずにセットアップするすべてのサーバーの役割を保持する場合は、**インプレース アップグレード**に移動する以前のオペレーティング システムから新しいバージョンの設定]、[サーバーの役割を維持したいです。、とデータをそのままです。 たとえば、サーバーが Windows Server 2012 R2 を実行している場合は、Windows Server 2016 または Windows Server 2019 にアップグレードできます。 ただし、すべての古いオペレーティング システムが、すべての新しいオペレーティング システムに移行できるわけではありません。 利用可能なアップグレード パスの次の図を参照してください。

![Windows Server では、インプレース アップグレード パスの図](media/upgrade-paths.png)

ステップ バイ ステップのガイダンスについてのアップグレードでは、 [Windows Server のアップグレード センター](http://aka.ms/upgradecenter)を参照してください。

<a href="http://aka.ms/upgradecenter"><img src="media/upgrade-center.png" alt="Screenshot of Windows Upgrade Center" title="Windows Server のアップグレード センター"></a>

## クラスター OS のローリング アップグレード
クラスター OS のローリング アップグレードには、Windows Server 2012 R2 および Windows Server 2016 から、HYPER-V またはスケール アウト ファイル サーバーのワークロードを停止することがなく、クラスター ノードのオペレーティング システムをアップグレードすると、管理者ができるようにします。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 この新機能の詳細は、「[Cluster operating system rolling upgrade (クラスター オペレーティング システムのローリング アップグレード)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)」で説明されています。

## 移行

Windows Server の移行は、同じまたは新しいバージョンの Windows Server を実行している別のコンピューターを Windows Server を実行しているソース コンピューターから、一度に 1 つの役割または機能を移行するときです。 これらのドキュメントで "移行" とは、同じコンピューター上でのアップグレードではなく、役割や機能、データを別のコンピューターに移動することを指します。 

## ライセンス変換
一部のオペレーティング システム リリースでは、簡単なコマンドと適切なライセンス キーにより、1 回の手順で特定のリリース エディションを同じリリースの別のエディションに変換できます。 これを**ライセンス変換**と呼びます。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。 一部の Windows Server のリリースでは、OEM 版、ボリューム ライセンス版、製品版の間を同じコマンドと適切なキーによって自由に変換できます。


 
 
