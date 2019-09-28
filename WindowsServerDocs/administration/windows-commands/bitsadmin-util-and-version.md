---
title: bitsadmin util とバージョン
description: '**Bitsadmin util とバージョン**の Windows コマンドに関するトピックでは、BITS サービスのバージョンが表示されます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 495ef17bbf6f39f20f6729b64de4b4bec0f9a3c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380199"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util とバージョン

BITS サービスのバージョン (2.0 など) を表示します。

**BITSAdmin 1.5 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>コメント

**Verbose**スイッチは次の処理を実行します。
-   各 BITS 関連の DLL のファイルバージョンを表示します。
-   BITS サービスを開始できることを確認します。
-   ビットグループポリシー値を表示します (Windows Vista のみ)

## <a name="BKMK_examples"></a>例

次の例では、BITS サービスのバージョンを示しています。
```
C:\>bitsadmin /Util /Version
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)