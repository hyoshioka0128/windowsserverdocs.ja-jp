---
title: bitsadmin rawreturn
description: '**Bitsadmin rawreturn**の Windows コマンドに関するトピックでは、解析に適したデータが返されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8cd84b6082b1fda8061ee7b324dd66991d3b206
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849885"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

解析に適したデータを返します。 通常、このコマンドは、値のみを受信するために、 **/create**および **/get*** スイッチと組み合わせて使用します。 このスイッチは、他のスイッチの前に指定する必要があります。

## <a name="syntax"></a>構文

```
bitsadmin /rawreturn
```

## <a name="remarks"></a>コメント

- 改行文字と書式設定を出力から取り除きます。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態の生データを取得します。

```
C:\>bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)