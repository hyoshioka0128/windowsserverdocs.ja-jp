---
title: exec
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f10e28a8da96bc7228af4561fb36824899f2d7a4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725742"
---
# <a name="exec"></a>exec



ローカルコンピューター上のファイルを実行します。 このファイルは、 **cmd**スクリプトにすることができます。

## <a name="syntax"></a>構文

```
exec <ScriptFile.cmd>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ScriptFile>|実行するスクリプトファイルを指定します。|

## <a name="remarks"></a>Remarks

-   このコマンドは、バックアップまたは復元シーケンスの一部としてデータを複製または復元するために使用されます。
-   スクリプトが失敗した場合は、エラーが返され、DiskShadow が終了します。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)