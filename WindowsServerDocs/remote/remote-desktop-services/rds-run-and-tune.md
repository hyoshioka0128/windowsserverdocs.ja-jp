---
title: RDS での実行と調整
description: リモート デスクトップ サービスの管理情報を提供します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 02/08/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79909767-a4c3-4ecf-8d3f-77d37a663153
author: spatnaik
manager: scottman
ms.openlocfilehash: 40f8dbd560da359e8764ed715e7776cc2d230a7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862183"
---
# <a name="run-and-tune-your-remote-desktop-services-environment"></a>実行し、リモート デスクトップ サービス環境を調整

配置のチューニング時間がかかり、インストルメンテーションおよび監視が必要です。 リモート デスクトップの展開を絞り込む、実行の維持、および必要に応じてスケール アウト (とスケールイン) のスケールを有効にするのには、次の手順を使用します。 

継続的に評価メトリックと実行中のコストに対して分散することをお勧めします。

## <a name="management-and-monitoring"></a>管理と監視

チェック アウト[RDS コレクション内のユーザーを管理する](rds-user-management.md)デスクトップとリモート リソースへのアクセスを管理する方法についてはします。

使用**Microsoft Operations Management Suite (OMS)** を潜在的なボトルネックのリモート デスクトップの展開を監視し、次の方法のいずれかを使用して管理します。 

- **サーバー マネージャー**:最大 500 の同時リモート エンドユーザーと展開を管理する Windows Server に組み込まれている RD 管理ツールを使用します。 
- **PowerShell**:最大 5000 の同時リモート エンドユーザーと展開を管理するのにには、Windows Server の場合にも組み込まれている、RD PowerShell モジュールを使用します。

## <a name="scale-bigger-better-faster"></a>スケール:大きいより良い、速い

デプロイに可視性より高い精度とスケールを制御できます。 簡単に追加またはリモート デスクトップ ホスト サーバーをスケールのニーズに基づいて削除します。 

Azure で構築されているリモート デスクトップの展開と、オンデマンドで自動的にスケーリングする Azure SQL と同様に、Azure サービスの使用します。

## <a name="automation-script-for-success"></a>Automation:成功のためのスクリプト

実行中、高度に拡張アプリケーションの保守には、定期的に操作を繰り返す必要があります。 必要なときに複数のデプロイで実行できるスクリプトを作成するのにには、リモート デスクトップ サービスの PowerShell コマンドレットと WMI プロバイダーを使用します。 デプロイ、デプロイを調整するには、リモート デスクトップ サービスのベスト プラクティス アナライザー (BPA) 規則を実行します。

## <a name="load-testing-avoid-surprises"></a>ロード テストします。予想外の問題を回避します。

負荷は、ストレス テストと実際の使用状況のシミュレーションの両方で展開をテストします。 防ぎ読み込みサイズによって異なります。 応答性がユーザーの要件を満たしていること、また、システム全体が回復力のあることを確認します。 シミュレーションなどのツール、LoginVSI、ユーザーのニーズに合わせて、デプロイの機能を確認するには、ロード テストを作成します。 