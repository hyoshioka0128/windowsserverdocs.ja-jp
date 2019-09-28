---
title: クオータの管理
description: この記事では、クォータの作成方法と管理方法について説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5a655e28020d08bb1c10fa862c007f914a8cf566
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403075"
---
# <a name="quota-management"></a>クオータの管理

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ファイル サーバー リソース マネージャー Microsoft<sup>®</sup> 管理コンソール (MMC) スナップインの **[クォータの管理]** ノードでは、次の作業を実行できます。

-   ボリュームまたはフォルダーで許可する領域を制限するクォータを作成し、クォータの制限値に近づくか、これを超えた場合に、通知を生成する。
-   ボリュームまたはフォルダー内のすべての既存のサブフォルダー、および将来作成されるすべてのサブフォルダーに適用される自動適用クォータを生成する。
-   新しいボリュームまたはフォルダーに容易に適用でき、組織全体で利用できる、クォータ テンプレートを定義する。

たとえば、次のようなことができます。

-   ユーザーの個人用サーバーフォルダーに200メガバイト (MB) の制限を設定します。これにより、ストレージの 180 MB を超えたときに、ユーザーとユーザーに電子メール通知が送信されます。
-   グループの共有フォルダーに対して、柔軟な 500 MB クォータを設定します。 この記憶域の上限に達すると、グループ内のすべてのユーザーに、記憶域クォータが一時的に 520 MB に拡張されたことを知らせる電子メールが送信されます。これにより、不要なファイルを削除し、事前設定された 500 MB クォータポリシーに準拠することができます。
-   一時フォルダーの使用量が 2 GB に達した時点で通知を受信するが、サーバーで実行されているサービスに必要であるため、そのフォルダーのクォータを制限しない。

ここでは、次のトピックについて説明します。

-   [クォータを作成する](create-quota.md)
-   [自動適用クォータを作成する](create-auto-apply-quota.md)
-   [クォータテンプレートを作成する](create-quota-template.md)
-   [クォータ テンプレートのプロパティを編集する](edit-quota-template-properties.md)
-   [自動適用クォータのプロパティを編集する](edit-auto-apply-quota-properties.md)

> [!Note]
> 電子メール通知やレポート機能を設定するには、まずファイル サーバー リソース マネージャーの全般的なオプションを設定する必要があります。

## <a name="see-also"></a>関連項目

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)


