---
title: bitsadmin setnotifycmdline
description: '**Bitsadmin setnotifycmdline**の Windows コマンドトピックでは、ジョブがデータの転送を終了したとき、またはジョブが状態に入ったときに実行されるコマンドラインコマンドを設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b268b68cbd355a7fe7f993d678a98f6fcb99f0ab
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122892"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

ジョブがデータの転送を終了したとき、またはジョブが指定された状態に入ったときに実行されるコマンドラインコマンドを設定します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /setnotifycmdline <job> <program_name> [program_parameters]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| program_name | ジョブの完了時に実行するコマンドの名前。 この値は NULL として設定できますが、その場合は*program_parameters*も null に設定する必要があります。 |
| program_parameters | *Program_name*に渡すパラメーター。 この値は NULL として設定できます。 *Program_parameters*が NULL に設定されていない場合は、 *program_parameters*の最初のパラメーターが*program_name*と一致している必要があります。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブが完了した後で notepad.exe を実行するためにサービスによって使用されるコマンドラインコマンドを設定します。

```
C:\>bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

```
C:\>bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)