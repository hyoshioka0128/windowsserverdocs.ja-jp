---
title: dispdiag
description: 表示情報をファイルに記録する dispdiag コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff4e3690ec3b2c9d473f05027d5637eda124d0ba
ms.sourcegitcommit: aed942d11f1a361fc1d17553a4cf190a864d1268
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235216"
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
