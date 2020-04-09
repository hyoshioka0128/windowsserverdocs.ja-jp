---
title: exec
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d39fbf948050dd00f329e461c34c2365030cb05d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844995"
---
# <a name="exec"></a>exec



ローカルコンピューター上のファイルを実行します。 このファイルは、 **cmd**スクリプトにすることができます。

## <a name="syntax"></a>構文

```
exec <ScriptFile.cmd>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ScriptFile >|実行するスクリプトファイルを指定します。|

## <a name="remarks"></a>コメント

-   このコマンドは、バックアップまたは復元シーケンスの一部としてデータを複製または復元するために使用されます。
-   スクリプトが失敗した場合は、エラーが返され、DiskShadow が終了します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)