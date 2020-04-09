---
title: bitsadmin util とバージョン
description: Bitsadmin util と version の Windows コマンドに関するトピックでは、BITS サービスのバージョンが表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 087cc1033166ab93e7496caaa7335433cafd6249
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848835"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util とバージョン

BITS サービスのバージョン (2.0 など) を表示します。

**BITSAdmin 1.5 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>コメント

**Verbose**スイッチは次の処理を実行します。
-   各 BITS 関連の DLL のファイルバージョンを表示します。
-   BITS サービスを開始できることを確認します。
-   ビットグループポリシー値を表示します (Windows Vista のみ)

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、BITS サービスのバージョンを示しています。
```
C:\>bitsadmin /Util /Version
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)