---
title: リセット
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c27ddd93d06670a30f797bd58dd396a9e7ce70a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835785"
---
# <a name="reset"></a>リセット



DiskShadow.exe を既定の状態にリセットします。 **リセット** はなどの複合 DiskShadow の操作を分離することで特に便利 **作成**, 、**インポート**, 、**バックアップ**, 、または **復元**します。

## <a name="syntax"></a>構文

```
reset
```

## <a name="remarks"></a>コメント

-   使用すると、 **リセット** コマンドなどのコマンドの状態を紛失した **追加**, 、**設定**, 、**ロード**, 、または **ライター**します。 **リセット**では、IVssBackupComponent インターフェイスも解放され、非永続的なシャドウコピーは失われます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)