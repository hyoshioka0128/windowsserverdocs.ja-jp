---
title: 復元をシミュレートします。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6652fea4e74c706fcc03b8a547fab771a7c0191
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370883"
---
# <a name="simulate-restore"></a>復元をシミュレートします。



発行することがなく、コンピューター上の復元のセッション内のライターをテスト **復元前** または **PostRestore** ライターへのイベントです。

## <a name="syntax"></a>構文

```
simulate restore
```

## <a name="remarks"></a>コメント

-   **復元をシミュレート** ライタ搭載の復元を成功させるために動作しているかどうかをテストするために使用します。
-   使用する前に **リストアをシミュレート**, を使用して、DiskShadow メタデータ ファイルを読み込む必要があります、 **メタデータの読み込み** コマンドです。 これには、選択されているライターと復元のコンポーネントが読み込まれます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)