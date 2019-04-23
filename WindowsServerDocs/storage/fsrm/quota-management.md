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
ms.openlocfilehash: febcd6ab0744a7fddd024e1f0afdb93711e8939a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829543"
---
# <a name="quota-management"></a>クオータの管理

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 の Windows Server (半期チャネル)

ファイル サーバー リソース マネージャー Microsoft<sup>®</sup> 管理コンソール (MMC) スナップインの **[クォータの管理]** ノードでは、次の作業を実行できます。

-   ボリュームまたはフォルダーで許可する領域を制限するクォータを作成し、クォータの制限値に近づくか、これを超えた場合に、通知を生成する。
-   ボリュームまたはフォルダー内のすべての既存のサブフォルダー、および将来作成されるすべてのサブフォルダーに適用される自動適用クォータを生成する。
-   新しいボリュームまたはフォルダーに容易に適用でき、組織全体で利用できる、クォータ テンプレートを定義する。

たとえば、次のようなことができます。

-   180 MB のストレージが制限を超過した場合に、ユーザーに送信される電子メール通知をユーザーの個人用サーバー フォルダーに 200 メガバイト (MB) 制限を設定します。
-   グループの共有フォルダーで柔軟な 500 MB のクォータを設定します。 この記憶域の上限に達すると、グループ内のすべてのユーザーは、記憶域のクォータが拡張されている一時的に 520 mb まで不要なファイルを削除して、事前設定された 500 MB のクォータ ポリシーに準拠できます電子メールで通知されます。
-   一時フォルダーの使用量が 2 GB に達した時点で通知を受信するが、サーバーで実行されているサービスに必要であるため、そのフォルダーのクォータを制限しない。

ここでは、次のトピックについて説明します。

-   [クォータを作成します。](create-quota.md)
-   [作成、自動適用クォータ](create-auto-apply-quota.md)
-   [クォータ テンプレートを作成します。](create-quota-template.md)
-   [クォータ テンプレートのプロパティを編集します。](edit-quota-template-properties.md)
-   [編集の自動適用クォータのプロパティ](edit-auto-apply-quota-properties.md)

> [!Note]
> 電子メール通知やレポート機能を設定するには、まずファイル サーバー リソース マネージャーの全般的なオプションを設定する必要があります。

## <a name="see-also"></a>関連項目

-   [設定ファイル サーバー リソース マネージャーのオプション](setting-file-server-resource-manager-options.md)


