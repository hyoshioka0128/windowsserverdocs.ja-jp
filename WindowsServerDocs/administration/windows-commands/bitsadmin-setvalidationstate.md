---
title: bitsadmin setvalidationstate
description: Bitsadmin setvalidationstate コマンドの参照記事。このコマンドは、ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dcdbd017f225704fc20d0472346d98fd84bb2c0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881028"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setvalidationstate <job> <file_index> <TRUE|FALSE>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| ジョブ | ジョブの表示名または GUID。 |
| file_index | 0から開始します。 |
| TRUE または FALSE | **TRUE**を指定すると、指定したファイルのコンテンツの検証が有効になり、 **FALSE**の場合は無効になります。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブについて、ファイル2のコンテンツの検証の状態を TRUE に設定するには、次のようにします。

```
bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
