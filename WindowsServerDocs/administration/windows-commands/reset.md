---
title: reset
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8903c300d12a019f8fb4aef6d367131a195d034
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371460"
---
# <a name="reset"></a>reset



DiskShadow.exe を既定の状態にリセットします。 **リセット** はなどの複合 DiskShadow の操作を分離することで特に便利 **作成**, 、**インポート**, 、**バックアップ**, 、または **復元**します。

## <a name="syntax"></a>構文

```
reset
```

## <a name="remarks"></a>コメント

-   使用すると、 **リセット** コマンドなどのコマンドの状態を紛失した **追加**, 、**設定**, 、**ロード**, 、または **ライター**します。 **リセット**では、IVssBackupComponent インターフェイスも解放され、非永続的なシャドウコピーは失われます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)