---
title: "記憶域レポートの管理"
description: "この記事では、記憶域レポートを生成、スケジュール、および監視する方法について説明します。"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c0d750fd139865daa92319c1d1926dc5d36669b2
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="storage-reports-management"></a>記憶域レポートの管理

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ファイル サーバー リソース マネージャー Microsoft<sup>®</sup> 管理コンソール (MMC) スナップインの **[記憶域レポートの管理]** ノードでは、次のタスクを実行できます。

-   定期的な記憶域レポートをスケジュールし、ディスクの使用状況の傾向を特定する。
-   全ユーザーまたは選択したユーザー グループが承認されていないファイルを保存しようとするのを監視する。
-   記憶域レポートを即座に生成する。

たとえば、次のようなことができます。

-   毎週日曜日の深夜に実行されるようにレポートをスケジュールし、最近アクセスされたファイル (過去 2 日間) を含む一覧を生成できます。 この情報をもとに、週末の記憶域の活動を監視し、週末に自宅から接続するユーザーへの影響を最小限に抑えるように、サーバーのダウンタイムを計画できます。
-   サーバー上のあるボリューム内のすべての重複ファイルを特定するために、任意の時点でレポートを実行できます。これにより、データを損失することなくディスク領域をすばやく再利用できるようになります。
-   ファイル グループごとのファイル レポートを実行して、記憶域リソースが異なるファイル グループ間でどのようにセグメント化されているかを特定できます。 
-   または、所有者ごとのファイル レポートを実行して、各ユーザーが共有記憶域リソースをどの程度使用しているかを分析できます。

ここでは、次のトピックについて説明します。

-   [レポートのセットをスケジュールする](schedule-set-of-reports.md)
-   [オン デマンドでレポートを生成する](generate-reports-on-demand.md)

> [!Note]
> 電子メール通知や特定のレポート機能を設定するには、まずファイル サーバー リソース マネージャーの全般的なオプションを設定する必要があります。

## <a name="see-also"></a>関連項目

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)


