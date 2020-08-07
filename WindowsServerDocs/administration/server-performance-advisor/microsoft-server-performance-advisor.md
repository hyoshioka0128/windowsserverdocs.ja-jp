---
title: Microsoft Server Performance Advisor
description: Microsoft Server Performance Advisor
ms.assetid: 468ebcb3-9eaf-477c-ab10-e3f1b3ce63dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.topic: article
ms.openlocfilehash: 4ec0190c97c5afc761c27c7c3156380441951544
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895688"
---
# <a name="microsoft-server-performance-advisor"></a>Microsoft Server Performance Advisor

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 の展開のパフォーマンスの問題の診断に役立つ Microsoft Server Performance Advisor (SPA) をダウンロードします。 SPA は包括的な診断レポートとグラフを生成し、すぐに始めるための推奨事項の問題を分析し、是正措置を開発を提供します。

-   [Server Performance Advisor の概要](#bkmk-aboutspa)

-   [サーバー パフォーマンス アドバイザーをダウンロードします。](#bkmk-downloadspa)

-   [Server Performance Advisor ユーザー ガイド](server-performance-advisor-users-guide.md)

-   [Server Performance Advisor パック開発ガイド](server-performance-advisor-pack-development-guide.md)

## <a name="overview-of-server-performance-advisor"></a><a href="" id="bkmk-aboutspa"></a>Server Performance Advisor の概要

サーバー パフォーマンス アドバイザーは、2 つの部分、SPA フレームワークおよび SPA Advisor パックで構成されます。

### <a name="the-server-performance-advisor-framework"></a>Server Performance Advisor フレームワーク

このエンジンは、advisor パックで指定されたデータを収集する、Microsoft SQL Server データベースに収集されたデータを書き込んで、SPA の Advisor パックのスクリプトを実行する、IT が容易な環境を作成、および最終的なレポートが表示されます。 のみ、SPA framework SPA コンソールをインストールする必要があります。 SPA コンソールをリモートでテスト対象のサーバーにアクセスまたはテスト対象のサーバーにインストールされているスタンドアロン コンピューターにインストールすることもできます。

### <a name="server-performance-advisor-packs"></a>Server Performance Advisor パックに関するページ

SPA Advisor パックとは、一連のメタデータとの SQL スクリプト ファイルで構成されているすべてのチューニングの規則の中心です。 SPA は、次の Advisor パックが付属します。

-   コア OS advisor パックは、特別なサーバーの役割の独立した、一般的なオペレーティング システム関数のパフォーマンスを分析します。

-   インターネット インフォメーション サーバー (IIS) の advisor パックは、IIS のパフォーマンスを追跡します。

-   HYPER-V Advisor パックは、HYPER-V サーバー ロールの全般的なパフォーマンスを分析します。

    **メモ**Hyper-v Advisor パックは、ゲストオペレーティングシステムを分析しません。



-   Active directory advisor パックは、active directory ロールの全般的なパフォーマンスを分析します。

SPA は、Microsoft 以外の開発者のニーズに合わせて advisor パックを作成するには拡張可能なモデルも提供されます。

**メモ**SPA は、すべてのハードウェアおよびユーザーシナリオコンテキストを理解できません。 意思決定をサーバーに加えられたすべての潜在的な変更の結果を理解するのに役立つツールが用意されている推奨事項を使用する必要があります。



## <a name="download-server-performance-advisor"></a><a href="" id="bkmk-downloadspa"></a>サーバー パフォーマンス アドバイザーをダウンロードします。


サーバー パフォーマンス アドバイザーの Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 をダウンロードするのにには、次のリンクを使用します。

-   [Microsoft Server Performance Advisor 3.1 (32 ビット)](https://go.microsoft.com/fwlink/p/?linkid=327751)

-   [Microsoft Server Performance Advisor 3.1 (64 ビット)](https://go.microsoft.com/fwlink/p/?linkid=327752)

次のコマンドを使用して、CAB ファイル内のファイルを抽出できます。

-   x86 バージョンの場合:`extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_x86.cab`

-   x64 バージョンの場合:`extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_amd64.cab`

**注意**.Cab ファイルを抽出すると、SPA は階層ディレクトリ構造を維持して正常に機能する必要があります。 サーバーにインストールされている CAB ツールによって非運用時のディレクトリ構造抽出可能性があります。 階層的なディレクトリ構造を保持するためには、ファイルのディレクトリ構造を抽出する CAB 抽出ユーティリティ ツールを使用することができます。

CAB の展開ツールは、ファイルを正しく展開、サブフォルダーは抽出先フォルダーに自動的に表示されます。

### <a name="spa-prerequisites"></a>SPA の前提条件

SPA コンソールでは、次のソフトウェアがインストールされていることが必要です。

-   Microsoft .NET Framework 4

-   SQL Server 2008 R2 Express SP1 または Microsoft SQL Server 2008 R2 SP1

以降のバージョン互換性がある場合があります。 SPA コンソールを使用して、既知の製品の非互換性が表示されます。
