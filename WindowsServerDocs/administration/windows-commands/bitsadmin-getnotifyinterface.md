---
title: bitsadmin getnotifyinterface
description: Bitsadmin getnotifyinterface コマンドの参照記事。指定されたジョブの COM コールバックインターフェイスを別のプログラムが登録したかどうかを判断します。
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0e22b240f16aa417cf46b715527cd9098c60794
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894061"
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
