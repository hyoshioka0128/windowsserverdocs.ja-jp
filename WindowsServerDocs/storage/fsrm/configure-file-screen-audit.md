---
title: ファイル スクリーンの監査を構成する
description: この記事では、ファイル スクリーン処理の監査レポートを生成するファイル スクリーンの監査を構成する方法を説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: cf1824e514c34ee89870daa6d15190bffd822a8b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475319"
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

## <a name="additional-references"></a>その他のリファレンス

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)
-   [記憶域レポートの管理](storage-reports-management.md)