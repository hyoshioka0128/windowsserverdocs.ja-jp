---
title: recover
description: 回復コマンドの参照記事。このコマンドは、不良ディスクまたは不良ディスクから読み取り可能な情報を回復します。
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c3d709d76743df4c1a653f0f0a19e8319b0e0f1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884314"
---
# <a name="recover"></a>recover

正しくないか欠陥があるディスクから読み取り可能な情報を復元します。 このコマンドは、ファイルをセクターごとに読み取り、適切なセクターからデータを回復します。 不良セクターのデータは失われます。 ファイルを回復するときに不良セクターのすべてのデータが失われたために、一度に 1 つのファイルを回復する必要があります。

**Chkdsk**コマンドによって報告された不良セクターは、ディスクの操作準備が整ったときに不良とマークされました。 これらに問題ありません、および **回復** 影響しません。

## <a name="syntax"></a>構文

```
recover [<drive>:][<path>]<filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `[<drive>:][<path>]<filename>` | 回復するファイル名 (現在のディレクトリにない場合はファイルの場所) を指定します。 *ファイル名*が必要です。ワイルドカードはサポートされていません。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

ファイル*story.txt*を回復する*には、* 次のように入力します。

```
recover d:\fiction\story.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
