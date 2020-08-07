---
title: bitsadmin getvalidationstate
description: Bitsadmin getvalidationstate コマンドの参照記事。ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b44fd90e2a35f5daf382cf506f7f68ae3c3ff1d9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893813"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| file_index | 0から開始します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブ内のファイル2のコンテンツの検証状態を取得するには、次のようにします。

```
bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
