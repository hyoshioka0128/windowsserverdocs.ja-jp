---
title: クオータの管理
description: この記事では、クォータの作成方法と管理方法について説明します。
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6effaf7c2d197c08b4930e09c3ada96462b17d6f
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476188"
---
# <a name="quota-management"></a>クオータの管理

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ファイル サーバー リソース マネージャー Microsoft<sup>®</sup> 管理コンソール (MMC) スナップインの **[クォータの管理]** ノードでは、次の作業を実行できます。

-   ボリュームまたはフォルダーで許可する領域を制限するクォータを作成し、クォータの制限値に近づくか、これを超えた場合に、通知を生成する。
-   ボリュームまたはフォルダー内のすべての既存のサブフォルダー、および将来作成されるすべてのサブフォルダーに適用される自動適用クォータを生成する。
-   新しいボリュームまたはフォルダーに容易に適用でき、組織全体で利用できる、クォータ テンプレートを定義する。

たとえば、次のようなことができます。

-   180 MB のストレージが制限を超過した場合に、ユーザーに送信される電子メール通知をユーザーの個人用サーバー フォルダーに 200 メガバイト (MB) 制限を設定します。
-   グループの共有フォルダーで柔軟な 500 MB のクォータを設定します。 この記憶域の上限に達すると、グループ内のすべてのユーザーは、記憶域のクォータが拡張されている一時的に 520 mb まで不要なファイルを削除して、事前設定された 500 MB のクォータ ポリシーに準拠できます電子メールで通知されます。
-   一時フォルダーの使用量が 2 GB に達した時点で通知を受信するが、サーバーで実行されているサービスに必要であるため、そのフォルダーのクォータを制限しない。

ここでは、次のトピックについて説明します。

-   [クォータを作成する](create-quota.md)
-   [自動適用クォータを作成する](create-auto-apply-quota.md)
-   [クォータ テンプレートを作成します。](create-quota-template.md)
-   [クォータ テンプレートのプロパティを編集する](edit-quota-template-properties.md)
-   [自動適用クォータのプロパティを編集する](edit-auto-apply-quota-properties.md)

> [!Note]
> 電子メール通知やレポート機能を設定するには、まずファイル サーバー リソース マネージャーの全般的なオプションを設定する必要があります。

## <a name="see-also"></a>関連項目

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)


