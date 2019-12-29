---
title: wbadmin のディスクの取得
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 320edef1-df11-446b-a183-9f81811ef938
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3440e061a97e54c32179ef7d71f469093e9fae00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362417"
---
# <a name="wbadmin-get-disks"></a>wbadmin のディスクの取得



ローカルコンピューターで現在オンラインになっている内部ディスクと外部ディスクの一覧を表示します。

このサブコマンドを使用してオンラインになっているディスクを一覧表示するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin get disks
```

## <a name="parameters"></a>パラメーター

このサブコマンドにはパラメーターがありません。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBDisk](https://technet.microsoft.com/library/jj902446.aspx)コマンドレット