---
title: reset
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0bd9b6735697cbcefdcf68dc3d4a53a6870a7a76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850963"
---
# <a name="reset"></a>reset



DiskShadow.exe を既定の状態にリセットします。 **リセット** はなどの複合 DiskShadow の操作を分離することで特に便利 **作成**, 、**インポート**, 、**バックアップ**, 、または **復元**します。

## <a name="syntax"></a>構文

```
reset
```

## <a name="remarks"></a>注釈

-   使用すると、 **リセット** コマンドなどのコマンドの状態を紛失した **追加**, 、**設定**, 、**ロード**, 、または **ライター**します。 **リセット**も IVssBackupComponent インターフェイスを解放し、非永続的なシャドウ コピーを失った。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)