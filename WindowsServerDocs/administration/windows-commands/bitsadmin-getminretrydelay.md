---
title: bitsadmin getminretrydelay
description: Bitsadmin getminretrydelay コマンドのリファレンストピックでは、ファイルの転送を試行する前に、サービスが一時的なエラーを検出した後に待機する時間 (秒単位) を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a50b9d98fe0b873dc58b8e86dc672a8f4157208a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717846"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

ファイルの転送を試行する前に、サービスが一時的なエラーを検出した後に待機する時間 (秒単位) を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの最小再試行間隔を取得するには、次のようにします。

```
bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
