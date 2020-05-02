---
title: bitsadmin getnotifyinterface
description: Bitsadmin getnotifyinterface コマンドのリファレンストピックでは、指定されたジョブの COM コールバックインターフェイスを別のプログラムが登録したかどうかを判断します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2158759067010292ca213f97014857354247b9c7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717736"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

別のプログラムによって、指定されたジョブの COM コールバックインターフェイス (notify インターフェイス) が登録されているかどうかを判断します。

## <a name="syntax"></a>構文

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

#### <a name="output"></a>出力

このコマンドの出力では、**登録済み**または登録**解除**済みのいずれかが表示されます。

> [!NOTE]
> コールバックインターフェイスを登録したプログラムを特定することはできません。

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの通知インターフェイスを取得するには、次のようにします。

```
bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
