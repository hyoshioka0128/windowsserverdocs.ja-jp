---
title: RDS - リモート デスクトップ サービス環境の実行と調整
description: リモート デスクトップ サービスの管理情報を提供します。
ms.author: spatnaik
ms.date: 02/08/2017
ms.topic: article
ms.assetid: 79909767-a4c3-4ecf-8d3f-77d37a663153
author: spatnaik
manager: scottman
ms.openlocfilehash: 2b7443255f5490a0b67633abbc9ea5bbb6a5bb82
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954889"
---
# <a name="run-and-tune-your-remote-desktop-services-environment"></a>リモート デスクトップ サービス環境の実行と調整

展開の調整には時間がかかり、インストルメンテーションと監視が必要です。 以下のプロセスを使用してリモート デスクトップの展開を調整し、実行を維持し、必要に応じてスケールアウト (およびスケールイン) できるようにします。

メトリックを継続的に評価し、ランニング コストとのバランスを取ることをお勧めします。

## <a name="management-and-monitoring"></a>管理と監視

デスクトップやリモート リソースへのアクセスを管理する方法については、「[RDS コレクションでのユーザーの管理](rds-user-management.md)」を参照してください。

**Microsoft Operations Management Suite (OMS)** を使用してリモート デスクトップの展開の潜在的なボトルネックを監視し、次のいずれかの方法でそれらを管理します。

- **サーバー マネージャー**:Windows Server に組み込まれている RD 管理ツールを使用して、最大 500 人の同時リモート エンドユーザーを含む展開を管理します。
- **PowerShell**:RD PowerShell モジュール (これも Windows Server にも組み込まれています) を使用して、最大 5000 人の同時リモート エンドユーザーを含む展開を管理します。

## <a name="scale-bigger-better-faster"></a>スケール:より大きく、よく、速く

展開を可視化することで、より正確にスケールを制御できます。 スケールのニーズに基づいて、リモート デスクトップ ホスト サーバーを簡単に追加または削除できます。

Azure 上に構築されたリモート デスクトップの展開では、Azure SQL などの Azure サービスを利用して、オンデマンドで自動的にスケールできます。

## <a name="automation-script-for-success"></a>オートメーション:成功のためのスクリプト

実行中の大規模なアプリケーションを維持するには、定期的な繰り返し操作が必要です。 リモート デスクトップ サービス PowerShell コマンドレットと WMI プロバイダーを使用して、必要に応じて複数の展開で実行できるスクリプトを開発します。 展開を調整するには、展開に対してリモート デスクトップ サービスのベスト プラクティス アナライザー (BPA) 規則を実行します。

## <a name="load-testing-avoid-surprises"></a>負荷テスト:予想外の問題を回避する

ストレス テストと実際の使用状況のシミュレーションの両方で展開の負荷テストを行います。 防ぎ読み込みサイズによって異なります。 応答性がユーザーの要件を満たしていること、また、システム全体が回復力のあることを確認します。 シミュレーションなどのツール、LoginVSI、ユーザーのニーズに合わせて、デプロイの機能を確認するには、ロード テストを作成します。