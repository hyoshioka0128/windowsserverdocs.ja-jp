---
title: bitsadmin setnotifycmdline
description: Bitsadmin setnotifycmdline コマンドの参照記事。ジョブがデータの転送を終了したとき、またはジョブが状態に入ったときに実行されるコマンドラインコマンドを設定します。
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a81b4521d8c765d85e6b4a92d0429b128f43198e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893001"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

ジョブがデータの転送を終了した後、またはジョブが指定された状態になった後に実行されるコマンドラインコマンドを設定します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /setnotifycmdline <job> <program_name> [program_parameters]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| program_name | ジョブの完了時に実行するコマンドの名前。 この値は NULL として設定できますが、その場合は*program_parameters*も null に設定する必要があります。 |
| program_parameters | *Program_name*に渡すパラメーター。 この値は NULL として設定できます。 *Program_parameters*が NULL に設定されていない場合は、 *program_parameters*の最初のパラメーターが*program_name*と一致している必要があります。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの完了時に Notepad.exe を実行するには、次のようにします。

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

Notepad.exe に EULA のテキストを表示するには、myDownloadJob という名前のジョブが完了します。

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
