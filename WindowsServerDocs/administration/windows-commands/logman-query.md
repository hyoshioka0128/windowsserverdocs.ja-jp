---
title: logman query
description: データコレクターまたはデータコレクターセットのプロパティを照会する logman クエリコマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2cb324651001f071e45acf0821f402458ed838d8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887285"
---
# <a name="logman-query"></a>logman query

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データコレクターまたはデータコレクターセットのプロパティを照会します。

## <a name="syntax"></a>構文

```
logman query [providers|Data Collector Set name] [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -s `<computer name>` | 指定したリモートコンピューターでコマンドを実行します。 |
| -config`<value>` | コマンドオプションを含む設定ファイルを指定します。 |
| [-n]`<name>` | 対象オブジェクトの名前。 |
| -/ | イベントトレースセッションに直接コマンドを送信します。保存もスケジュールもされません。 |
| /? | 状況依存のヘルプを表示します。 |

### <a name="examples"></a>例

ターゲットシステムで構成されているすべてのデータコレクターセットを一覧表示するには、次のように入力します。

```
logman query
```

*Perf_log*という名前のデータコレクターセットに含まれているデータコレクターの一覧を表示するには、次のように入力します。

```
logman query perf_log
```

ターゲットシステム上のデータコレクターの使用可能なすべてのプロバイダーを一覧表示するには、次のように入力します。

```
logman query providers
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman コマンド](logman.md)
