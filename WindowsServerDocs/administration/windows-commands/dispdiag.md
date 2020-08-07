---
title: dispdiag
description: 表示情報をファイルに記録する dispdiag コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78b8080395fa30a934d1a9380bf86beae7e62dc0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890826"
---
# <a name="dispdiag"></a>dispdiag

ログには、ファイルの情報が表示されます。

## <a name="syntax"></a>構文

```
dispdiag [-testacpi] [-d] [-delay <seconds>] [-out <filepath>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -testacpi | ホットキー診断テストを実行します。 テスト中に押されたキーのキー名、コード、およびスキャンコードを表示します。 |
| -d | テスト結果と共にダンプファイルを生成します。 |
| -delay`<seconds>` | 指定された時間 *(秒単位)* でデータの収集を遅らせます。 |
| -out`<filepath>`  | 収集したデータを保存するパスとファイル名を指定します。 これは、最後のパラメーターである必要があります。 |
| -? | 使用可能なコマンドパラメーターを表示し、それらを使用するためのヘルプを提供します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
