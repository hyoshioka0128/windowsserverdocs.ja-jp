---
title: ファイル管理タスク
description: この記事では、ファイル管理タスクを自動化するプロセスについて説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 402af4bd7c00bedfc3d01d43071af4fcd374d428
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473999"
---
# <a name="file-management-tasks"></a>ファイル管理タスク

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、windows server 2012 R2、windows Server 2012、Windows Server 2008 R2

ファイル管理タスクは、サーバー上のファイルのサブセットの検出と簡単なコマンドを適用するプロセスを自動化します。 繰り返しの手間を減らすために、これらのタスクを定期的に行うようにスケジュールすることができます。 ファイル管理タスクによって処理できるファイルは、次のプロパティを使用して定義できます。

-   場所
-   分類プロパティ
-   作成日時
-   変更日時
-   最終アクセス日時

ファイル管理タスクは、何らかのポリシーの適用が迫っているファイルの所有者に対して、そのことを通知するように設定することもできます。

> [!Note]
> 個々のファイル管理タスクは、独立したスケジュールで実行されます。

<br />
ここでは、次のトピックについて説明します。

-   [ファイルの有効期限タスクを作成する](create-file-expiration-task.md)
-   [カスタム ファイル管理タスクを作成する](create-custom-file-management-task.md)

> [!Note]
> 電子メール通知や特定のレポート機能を設定するには、まずファイル サーバー リソース マネージャーの全般的なオプションを設定する必要があります。

## <a name="additional-references"></a>その他のリファレンス

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)


