---
title: reset
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0701324ad1ee94cc645c7519d81fef7357b6a34a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722353"
---
# <a name="reset"></a>reset



DiskShadow.exe を既定の状態にリセットします。 **リセット** はなどの複合 DiskShadow の操作を分離することで特に便利 **作成**, 、**インポート**, 、**バックアップ**, 、または **復元**します。

## <a name="syntax"></a>構文

```
reset
```

## <a name="remarks"></a>Remarks

-   使用すると、 **リセット** コマンドなどのコマンドの状態を紛失した **追加**, 、**設定**, 、**ロード**, 、または **ライター**します。 **リセット**では、IVssBackupComponent インターフェイスも解放され、非永続的なシャドウコピーは失われます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)