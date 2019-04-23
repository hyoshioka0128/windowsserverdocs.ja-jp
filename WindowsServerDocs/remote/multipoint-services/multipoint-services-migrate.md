---
title: MultiPoint Services in Windows Server 2016 への移行します。
description: MultiPoint Services の以前のバージョンから移行する方法について説明します
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16c217ad-700a-48a3-8398-4a7f7e9edb52
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 24c35c31bf920c41bafa16901ee30a023565dad8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861203"
---
# <a name="multipoint-services-migration-in-windows-server-2016"></a>Windows Server 2016 で multiPoint Services の移行
>適用先:Windows Server 2016

Windows Server 2016 の MultiPoint Services の以前のリリースから MultiPoint Services の RTM バージョンに移行できます。 次の情報には、準備情報や移行と検証の手順が説明します。

ドキュメントや移行ツールは、サーバーの役割設定と Windows Server 2016 を実行している移行先サーバーに既存のサーバーからのデータの移行を容易になります。 このガイドで説明されている手順を使用すると、移行プロセスを簡素化すること、移行時間を短縮すること、移行プロセスの精度を高めること、および移行プロセス中に発生する可能性のある競合を取り除くことができます。 

## <a name="what-to-know-before-you-begin"></a>使い始める前に
移行プロセスを開始する前に、次の点を注意してください。

- 移行プロセスは、自動的に収集または MultiPoint サービスの役割でのアプリケーション設定を記録します。 すべてのアプリケーションを移行するためのカスタマイズされた移行計画を作成する必要があります。 これは、MultiPoint Services での仮想デスクトップ機能を使用する場合にも当てはまります。
- このガイドは、データの移動のガイダンスがユーザーに保存または MultiPoint サーバー上の共有フォルダーには提供されません。 これは通常のステーションと仮想デスクトップに当てはまりますステーションです。
- このガイドでは、移行元サーバーには、複数のロールが実行されているときに移行する方法については含まれません。 サーバーで複数のロールが実行されている場合は、役割の移行ガイドで提供される情報に基づいて、サーバー環境に固有のカスタムの移行手順を設計する必要があります。
- このガイドでは、移行のリモート デスクトップ サービス CAL 情報は含まれません。 詳細については、次を参照してください。[移行リモート デスクトップ サービス クライアント アクセス ライセンス (RDS Cal)](https://technet.microsoft.com/library/dd851844.aspx)します。

## <a name="supported-migration-scenarios-for-multipoint-services-in-windows-server-2016"></a>Windows Server 2016 で MultiPoint Services のサポートされている移行シナリオ
MultiPoint サービスの役割サービスは、Windows Server 2016 Standard および Datacenter で使用できます。 この移行ガイドでは、Multipoint サービスの役割サービスを同じバージョンを実行している移行先サーバーに Windows Server 2016 を実行している移行元サーバーから移行する方法について説明します。

## <a name="scenarios-that-are-not-supported"></a>サポートされていないシナリオ

次の移行シナリオはサポートされていません。

- 移行または Windows MultiPoint Server 2012 および 2011 からアップグレードします。
- 移行元サーバーから別のシステム UI 言語がインストールされていると、オペレーティング システムで実行されている移行先サーバーへの移行。
- 物理サーバーから仮想マシンへの MultiPoint サービスの役割サービスを移行します。
- MultiPoint Server からアプリケーションまたはアプリケーションの設定を移行します。

## <a name="the-impact-of-migration-on-multipoint-services"></a>MultiPoint Services での移行の影響
MultiPoint サービスの役割は使用できないこと、移行中にあります。 ダウンタイムを最小限に抑え、ユーザーに与える影響を軽減するために、サーバーへのアクセスが混雑していない時間帯に移行を実行するように計画することができます。 その間はリソースを使用できなくなることをユーザーに通知してください。

## <a name="migration-information-and-steps"></a>移行情報と手順
MultiPoint Services の移行を計画して実現するには、次の情報を使用します。

- [移行のために必要な情報を収集します。](multipoint-services-migration-preparation.md)
- [MultiPoint サービスの役割サービスを移行します。](multipoint-services-migration-steps.md)
- [移行を検証して、移行後のクリーンアップ タスクを実行](multipoint-services-post-migration-steps.md)