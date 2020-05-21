---
title: exec
description: ローカルコンピューター上でスクリプトファイルを実行する exec コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 956f3d4a7c5992980aea0fc0f5933ee7def48381
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436108"
---
# <a name="exec"></a>exec

ローカルコンピューター上でスクリプトファイルを実行します。 このコマンドでは、バックアップまたは復元シーケンスの一部としてデータの複製または復元も実行されます。 スクリプトが失敗した場合は、エラーが返され、DiskShadow が終了します。

このファイルは、 **cmd**スクリプトにすることができます。

## <a name="syntax"></a>構文

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<scriptfile.cmd>` | 実行するスクリプトファイルを指定します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [diskshadow コマンド](diskshadow.md)
