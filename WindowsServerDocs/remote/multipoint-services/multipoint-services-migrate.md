---
title: Windows Server 2016 の MultiPoint Services への移行
description: 以前のバージョンの MultiPoint Services から移行する方法について説明します。
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 16c217ad-700a-48a3-8398-4a7f7e9edb52
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 1609ff02c8e1b1480d004104bdc7e37f1240729a
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959274"
---
# <a name="multipoint-services-migration-in-windows-server-2016"></a>Windows Server 2016 での MultiPoint サービスの移行
>適用先:Windows Server 2016

以前のリリースの Windows Server 2016 MultiPoint Services から、最新バージョンの MultiPoint services に移行できます。 次の情報は、準備情報と移行および検証の手順を示しています。

移行ドキュメントと移行ツールにより、既存のサーバーから Windows Server 2016 を実行している移行先サーバーへのサーバーの役割設定とデータの移行が容易になります。 このガイドで説明されている手順を使用すると、移行プロセスを簡素化すること、移行時間を短縮すること、移行プロセスの精度を高めること、および移行プロセス中に発生する可能性のある競合を取り除くことができます。 

## <a name="what-to-know-before-you-begin"></a>開始する前に理解しておくべきこと
移行プロセスを開始する前に、次の点に注意してください。

- 移行プロセスでは、MultiPoint Services ロールのアプリケーションの設定が自動的に収集または記録されることはありません。 移行するアプリケーションに対しては、カスタマイズされた移行計画を作成する必要があります。 これは、MultiPoint Services の仮想デスクトップ機能を使用する場合にも当てはまります。
- このガイドでは、ユーザーまたは MultiPoint サーバー上の共有フォルダーに保存されたデータを移動する方法については説明しません。 これは、通常のステーションと仮想デスクトップステーションに適用されます。
- 移行元サーバーで複数の役割が実行されている場合の移行方法については、このガイドには記載されていません。 サーバーで複数の役割が実行されている場合は、役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行手順を設計する必要があります。
- このガイドにはリモートデスクトップサービス CAL の移行に関する情報は含まれていません。 この情報については、「[移行リモートデスクトップサービスクライアントアクセスライセンス (RDS cal)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))」を参照してください。

## <a name="supported-migration-scenarios-for-multipoint-services-in-windows-server-2016"></a>Windows Server 2016 の MultiPoint Services でサポートされている移行シナリオ
MultiPoint サービスの役割サービスは、Windows Server 2016 Standard および Datacenter で使用できます。 この移行ガイドでは、Windows Server 2016 を実行している移行元サーバーから、同じバージョンを実行している移行先サーバーに Multipoint Services の役割サービスを移行する方法について説明します。

## <a name="scenarios-that-are-not-supported"></a>サポートされていないシナリオ

次の移行シナリオはサポートされていません。

- Windows MultiPoint Server 2012 および2011からの移行またはアップグレード。
- 異なるシステム UI 言語がインストールされているオペレーティングシステムでを実行している移行先サーバーに移行元サーバーから移行する場合。
- MultiPoint Services の役割サービスを物理サーバーから仮想マシンに移行しています。
- すべてのアプリケーションまたはアプリケーション設定を MultiPoint サーバーから移行します。

## <a name="the-impact-of-migration-on-multipoint-services"></a>MultiPoint Services での移行の影響
移行中は MultiPoint Services の役割を使用できないことに注意してください。 ダウンタイムを最小限に抑え、ユーザーに与える影響を軽減するために、サーバーへのアクセスが混雑していない時間帯に移行を実行するように計画することができます。 その間はリソースを使用できなくなることをユーザーに通知してください。

## <a name="migration-information-and-steps"></a>移行に関する情報と手順
MultiPoint サービスの移行を計画して実行するには、次の情報を使用します。

- [移行に必要な情報を収集します。](multipoint-services-migration-preparation.md)
- [MultiPoint Services の役割サービスを移行します。](multipoint-services-migration-steps.md)
- [移行を検証し、移行後のクリーンアップタスクを実行する](multipoint-services-post-migration-steps.md)
