---
title: 実行
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 514503e4920e16ba6778185af32f925541805223
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377434"
---
# <a name="exec"></a>実行



ローカルコンピューター上のファイルを実行します。 このファイルは、 **cmd**スクリプトにすることができます。

## <a name="syntax"></a>構文

```
exec <ScriptFile.cmd>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ScriptFile >|実行するスクリプトファイルを指定します。|

## <a name="remarks"></a>コメント

-   このコマンドは、バックアップまたは復元シーケンスの一部としてデータを複製または復元するために使用されます。
-   スクリプトが失敗した場合は、エラーが返され、DiskShadow が終了します。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)