---
title: "クオータの管理"
description: "この記事では、クォータの作成方法と管理方法について説明します。"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 60436f12e07b8a3f16312829d53a2885c98f30ed
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="quota-management"></a>クオータの管理

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ファイル サーバー リソース マネージャー Microsoft<sup>®</sup> 管理コンソール (MMC) スナップインの **[クォータの管理]** ノードでは、次の作業を実行できます。

-   ボリュームまたはフォルダーで許可する領域を制限するクォータを作成し、クォータの制限値に近づくか、これを超えた場合に、通知を生成する。
-   ボリュームまたはフォルダー内のすべての既存のサブフォルダー、および将来作成されるすべてのサブフォルダーに適用される自動適用クォータを生成する。
-   新しいボリュームまたはフォルダーに容易に適用でき、組織全体で利用できる、クォータ テンプレートを定義する。

たとえば、次のようなことができます。

-   200 MB の制限をユーザーの個人用サーバー フォルダーに設定し、記憶域の使用率が 180 MB を超えたときに、管理者に通知を送信する。
-   グループの共有フォルダーに、柔軟な 500 MB のクォータを設定する。 この記憶域制限に達した場合、グループ内のすべてのユーザーはストレージ クォータが一時的に 520 MB まで拡張されたことを電子メールで通知されます。これにより、ユーザーは不要なファイルを削除して、現在の 500 MB のクォータ ポリシーに従うことができます。
-   一時フォルダーの使用量が 2 GB に達した時点で通知を受信するが、サーバーで実行されているサービスに必要であるため、そのフォルダーのクォータを制限しない。

ここでは、次のトピックについて説明します。

-   [クォータを作成する](create-quota.md)
-   [自動適用クォータを作成する](create-auto-apply-quota.md)
-   [クォータ テンプレートを作成する](create-quota-template.md)
-   [クォータ テンプレートのプロパティを編集する](edit-quota-template-properties.md)
-   [自動適用クォータのプロパティを編集する](edit-auto-apply-quota-properties.md)

> [!Note]
> 電子メール通知やレポート機能を設定するには、まずファイル サーバー リソース マネージャーの全般的なオプションを設定する必要があります。

## <a name="see-also"></a>関連項目

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)


