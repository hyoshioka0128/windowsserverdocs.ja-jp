---
title: ファイル スクリーンの監査を構成する
description: この記事では、ファイル スクリーン処理の監査レポートを生成するファイル スクリーンの監査を構成する方法を説明します。
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 822c483fc7f5f4518ca976b1f7d719b95730008f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950687"
---
# <a name="configure-file-screen-audit"></a>ファイル スクリーンの監査を構成する

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ファイル サーバー リソース マネージャーを使用することで、監査データベースにファイル スクリーン処理の動作を記録できます。 このデータベースに保存された情報は、ファイル スクリーン処理の監査レポートの生成に使用されます。

> [!Important]
> **[監査データベースにファイル スクリーン処理の動作状況を記録する]** チェック ボックスがオフの場合、ファイル スクリーン処理の監査レポートには何の情報も含まれません。

## <a name="to-configure-file-screen-audit"></a>ファイル スクリーンの監査を構成するには

1.  コンソール ツリーで、**[ファイル サーバー リソース マネージャー]** を右クリックし、**[オプションの構成]** をクリックします。 [**ファイル サーバー リソース マネージャーのオプション**] ダイアログ ボックスが開きます。

2.  **[ファイル スクリーンの監査]** タブで、**[監査データベースにファイル スクリーン処理の動作状況を記録する]** チェック ボックスをオンにします。

3.  **[OK]** をクリックします。 これで、すべてのファイル スクリーン処理が監査データベースに保存され、ファイル スクリーン処理の監査レポートを実行することによって表示できます。

## <a name="additional-references"></a>その他の参照情報

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)
-   [記憶域レポートの管理](storage-reports-management.md)