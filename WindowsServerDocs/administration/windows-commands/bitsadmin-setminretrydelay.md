---
title: bitsadmin setminretrydelay
description: Bitsadmin setminretrydelay コマンドのリファレンストピック。このコマンドは、ファイルの転送を試行する前に、BITS が一時的なエラーを検出した後に待機する時間の最小値を秒単位で設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fc54b4466d8f0bac12bd42ebf6c5e2c66087a15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720120"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

一時エラーが発生してからファイルの転送を試行するまでの待機時間の最小値を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setminretrydelay <job> <retrydelay>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| retrydelay | 転送中にエラーが発生した後のビットの待機時間の最小値 (秒単位)。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの最小再試行間隔を35秒に設定するには、次のようにします。

```
bitsadmin /setminretrydelay myDownloadJob 35
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
