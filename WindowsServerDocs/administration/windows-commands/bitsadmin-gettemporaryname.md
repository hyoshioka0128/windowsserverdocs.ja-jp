---
title: bitsadmin gettemporaryname
description: Bitsadmin gettemporary name コマンドの参照記事。ジョブ内の指定されたファイルの一時ファイル名を報告します。
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b5919d45f2b8497bb6e8fa6cf3650f49e27cd48
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893835"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

ジョブ内の指定されたファイルの一時ファイル名を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| file_index | 0から開始します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのファイル2の一時ファイル名を報告するには、次のようにします。

```
bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
