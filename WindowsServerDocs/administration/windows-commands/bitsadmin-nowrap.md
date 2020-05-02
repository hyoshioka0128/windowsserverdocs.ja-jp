---
title: bitsadmin nowrap
description: Bitsadmin nowrap コマンドのリファレンストピック。コマンドウィンドウの右端からはみ出た出力テキストの行をすべて切り捨てます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2aac604ec3e13026e322d7cb7a9364df46266a0c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717333"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

コマンドウィンドウの右端を超えて拡張する出力テキストの行をすべて切り捨てます。 既定では、**モニター**スイッチを除くすべてのスイッチが出力をラップします。 他のスイッチの前に、 **nowrap**スイッチを指定します。

## <a name="syntax"></a>構文

```
bitsadmin /nowrap
```

## <a name="examples"></a>例

出力をラップせずに*Mydownloadjob*という名前のジョブの状態を取得するには、次のようにします。

```
bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
