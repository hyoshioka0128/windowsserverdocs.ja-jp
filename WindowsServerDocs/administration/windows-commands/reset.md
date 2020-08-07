---
title: reset
description: 参照記事 * * * *-
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f491a3d8c805ac6b3558f3778f6eba91a7551b82
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883653"
---
# <a name="reset"></a>reset



DiskShadow.exe を既定の状態にリセットします。 **リセット** はなどの複合 DiskShadow の操作を分離することで特に便利 **作成**, 、**インポート**, 、**バックアップ**, 、または **復元**します。

## <a name="syntax"></a>構文

```
reset
```

## <a name="remarks"></a>Remarks

-   使用すると、 **リセット** コマンドなどのコマンドの状態を紛失した **追加**, 、**設定**, 、**ロード**, 、または **ライター**します。 **リセット**では、IVssBackupComponent インターフェイスも解放され、非永続的なシャドウコピーは失われます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)