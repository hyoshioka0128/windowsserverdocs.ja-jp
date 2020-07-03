---
title: bitsadmin getnotifyinterface
description: Bitsadmin getnotifyinterface コマンドの参照記事。指定されたジョブの COM コールバックインターフェイスを別のプログラムが登録したかどうかを判断します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c86b611eb5f46759c474171085884c5702e07d1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926904"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

別のプログラムによって、指定されたジョブの COM コールバックインターフェイス (notify インターフェイス) が登録されているかどうかを判断します。

## <a name="syntax"></a>構文

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
