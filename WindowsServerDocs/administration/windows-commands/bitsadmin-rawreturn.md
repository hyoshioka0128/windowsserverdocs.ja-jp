---
title: bitsadmin rawreturn
description: Bitsadmin rawreturn コマンドの参照記事。解析に適したデータを返します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b537b21678c100364406d4c59eaa02efd143e21
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926461"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

解析に適したデータを返します。 通常、このコマンドは、値のみを受信するために、 **/create**および **/get*** スイッチと組み合わせて使用します。 このスイッチは、他のスイッチの前に指定する必要があります。

> [!NOTE]
> このコマンドは、改行文字と書式設定を出力から取り除きます。

## <a name="syntax"></a>構文

```
bitsadmin /rawreturn
```

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの状態の生データを取得するには、次のようにします。

```
bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
