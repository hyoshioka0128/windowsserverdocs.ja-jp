---
title: bitsadmin gettemporaryname
description: Bitsadmin gettemporary name コマンドのリファレンストピックでは、ジョブ内の指定されたファイルの一時ファイル名を報告します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7780691f37fb78f1553fa993fd408d224be39ff
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717490"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

ジョブ内の指定されたファイルの一時ファイル名を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| file_index | 0から開始します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのファイル2の一時ファイル名を報告するには、次のようにします。

```
bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
