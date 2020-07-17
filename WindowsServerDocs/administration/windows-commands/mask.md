---
title: mask
description: Mask コマンドの参照記事。 import コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2839fce0a64f187c1445a5f6a4af6c5f0ebc9fb8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922109"
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

#### <a name="remarks"></a>注釈

- *ShadowSetID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

### <a name="examples"></a>例

インポートされたシャドウコピー *% Import_1%* を削除するには、次のように入力します。

```
mask %Import_1%
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)