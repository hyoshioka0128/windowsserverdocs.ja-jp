---
title: exit
description: コマンドインタープリターを終了する exit のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97068232a7ffa82e59ba486b449af96638e3d8f0
ms.sourcegitcommit: aed942d11f1a361fc1d17553a4cf190a864d1268
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235069"
---
# <a name="exit"></a>exit

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンドインタープリターまたは現在のバッチスクリプトを終了します。

## <a name="syntax"></a>構文

```
exit [/b] [<exitcode>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /b | Cmd.exe を終了する代わりに、現在のバッチスクリプトを終了します。 バッチスクリプトの外部から実行された場合は、Cmd.exe を終了します。 |
| `<exitcode>` | 数値を指定します。 **/B**が指定されている場合、ERRORLEVEL 環境変数はその数値に設定されます。 コマンドインタープリターを終了すると、プロセス終了コードはその番号に設定されます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

コマンドインタープリターを閉じるには、次のように入力します。

```
exit
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
