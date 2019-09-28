---
title: Windows 管理センター SDK ケーススタディ-DataON
description: Windows 管理センター SDK ケーススタディ-DataON
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 01/11/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0e4def5cd8a88cd5cb5d4df71d2f3a192ae23701
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406965"
---
# <a name="dataon-must-extension"></a>DataON には拡張機能が必要です

## <a name="integrated-monitoring-and-management-for-microsoft-hyper-converged-infrastructure"></a>Microsoft ハイパー集約型インフラストラクチャの統合された監視と管理

[Dataon](http://www.dataonstorage.com/)は、Microsoft Windows Server 環境向けに最適化された、ハイパー集約型インフラストラクチャおよびストレージシステムの業界最高レベルのプロバイダーです。 Microsoft アプリケーション、仮想化、データ保護、およびハイブリッドクラウドサービスの提供にのみ重点を置いているため、650を超えるエンタープライズデプロイと 120 PB を超える記憶域スペースダイレクトのデプロイがあります。

Windows 管理センター向けの[Dataon の](http://www.dataonstorage.com/must)拡張機能は、2つの補完的製品を統合して顧客に提供することによって、監視と管理、およびエンドツーエンドの洞察をハードウェアとソフトウェアの間でまとめて行うことができる値の代表的な例です。クラスター全体を統合されたエクスペリエンスで実現します。

> <cite>「スタンドアロンで可視性、監視、管理ツールを使用して、Windows 管理センター内で動作させることができました。お客様は、によって提供される拡張機能を活用できます。また、1つのコンソールからのと Windows 管理センターの組み合わせによって、Windows Server ベースのインフラストラクチャの究極の管理エクスペリエンスが提供されます。 "</cite>
>
> --Howard Lo、売上およびマーケティング担当副社長、DataON

次のような機能を提供することで、Windows 管理センターの機能を拡張する必要があります。
- **履歴データレポート**– IOPS、待機時間、クラスター上のスループット、記憶域プール、ボリューム、ノードなど、システムパフォーマンスデータのリアルタイムおよび月ごとのダッシュボードを提供します。
- **ディスクマッピング**–ノードのデバイスの種類とコンポーネントを表示し、ノード全体のディスクマップを明確にします。 ディスクの数、ディスクの種類、各ドライブの場所とスロット、およびディスクのヘルス状態が表示されます。
- **システムアラート**-Windows ヘルスサービス障害を利用して、ハードウェア障害、構成の問題、およびリソースの飽和度を特定します。 また、特定の場所、エラーの説明、および回復操作の複数レベルの評価も提供します。 また、サードパーティの SNMP 監視トラップを利用して、ディスクまたはハードウェアの交換が必要なときにアラートを通知することもできます。
- **SAN と同様の通話ホームサービス**–システムアラートによって、管理者は自動電子メールアラートを主要な連絡先に送信できます。

![*Windows 管理センターの dataon 拡張機能のディスクマッピングにおける dataon 拡張機能のディスクマッピング*](../../media/extend-case-study-dataon/dataon-1.png)


> <cite>"Windows 管理センターでは、同じコンソール内で両方のツールを使用できるようにする必要があるため、同じコンソール内で両方のツールを使用できるようにする必要があります。Windows 管理センターと DataON を組み合わせて使用すると、より効率的になり、チームの時間を節約することができます。これにより、管理者のタスクを前に行ったのと比べて、より迅速に実現できます。 "</cite>
>
> --Roper、テクノロジサポートサービスのファシリテータ、チェロキー郡 (GA) School 地区

![*Windows 管理センターの dataon 拡張機能警告サービスの dataon 拡張機能の警告サービス*](../../media/extend-case-study-dataon/dataon-2.png)


> <cite>「非常に貴重で、大きな販売ポイントでした。Microsoft では、Microsoft ハイパースレッディングインフラストラクチャをサポートするために DataON のコミットメントを実証しました。S2D アプライアンスでを含める必要があります。これは、実行可能な SAN 交換として記憶域スペースダイレクトでソリューションを完了するためのものです。 "</cite>
>
> --Benjamin Clements、社長、戦略的オンラインシステム、Inc.