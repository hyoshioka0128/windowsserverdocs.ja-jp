---
title: 作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 837aa449-9b60-41ae-9ef1-ef67af6e5918
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2245efb6c3bce8aecf8edf730694804ffbdc3d80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378777"
---
# <a name="create"></a>作成



現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始します。 シャドウコピーセットに少なくとも1つのボリュームが必要です。

## <a name="syntax"></a>構文

```
create
```

## <a name="remarks"></a>コメント

-   **Create**コマンドを使用する前に、 **[ボリュームの追加]** コマンドでボリュームを少なくとも1つ追加する必要があります。
-   **[バックアップの開始]** コマンドを使用すると、コピーバックアップではなく完全バックアップを指定できます。
-   **Create**コマンドを実行した後、 **exec**コマンドを使用して、シャドウコピーからバックアップ用の複製スクリプトを実行できます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)