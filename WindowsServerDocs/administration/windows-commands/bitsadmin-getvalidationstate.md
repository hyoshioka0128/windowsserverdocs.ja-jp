---
title: bitsadmin getvalidationstate
description: Bitsadmin getvalidationstate コマンドの参照記事。ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72d53572411a33259467fa8023b9ef08fe4a5595
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926629"
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
