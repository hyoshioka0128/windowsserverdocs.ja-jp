---
title: exec
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ecdfd05b8abefb35946b783daaa3220a6713a38d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882923"
---
# <a name="exec"></a>exec



ローカル コンピューター上のファイルを実行します。 ファイルは、 **cmd**スクリプト。

## <a name="syntax"></a>構文

```
exec <ScriptFile.cmd>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ScriptFile.cmd>|実行するスクリプト ファイルを指定します。|

## <a name="remarks"></a>注釈

-   このコマンドは、複製またはバックアップの一部としてデータを復元または復元シーケンスに使用されます。
-   スクリプトが失敗した場合、エラーが返され、DiskShadow を終了します。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)