---
title: exec
description: ローカルコンピューター上でスクリプトファイルを実行する exec コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4c9ff71b886bd84120bd3af7c1f8d8c143425da
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932309"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [diskshadow コマンド](diskshadow.md)
