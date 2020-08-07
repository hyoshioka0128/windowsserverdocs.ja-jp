---
title: mask
description: Mask コマンドの参照記事。 import コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a893d32dca90169d51a04db66b3dc796cbc69a46
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886528"
---
# <a name="mask"></a>mask

**インポート**コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。

## <a name="syntax"></a>構文

```
mask <shadowsetID>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| shadowsetID | 指定されたシャドウコピーセット ID に属するシャドウコピーを削除します。 |

#### <a name="remarks"></a>Remarks

- *ShadowSetID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

### <a name="examples"></a>例

インポートされたシャドウコピー *% Import_1%* を削除するには、次のように入力します。

```
mask %Import_1%
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)