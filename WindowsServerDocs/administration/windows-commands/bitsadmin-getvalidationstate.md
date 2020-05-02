---
title: bitsadmin getvalidationstate
description: Bitsadmin getvalidationstate コマンドのリファレンストピックでは、ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca753b20a1b7834d2e05d4ff8729a08332256f8c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717459"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| file_index | 0から開始します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブ内のファイル2のコンテンツの検証状態を取得するには、次のようにします。

```
bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
