---
title: makecab
description: Makecab コマンドの参照記事。既存のファイルをキャビネット (.cab) ファイルにパッケージ化します。
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a1052541b8455b082b001901e8374b4d7f5acaf
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887019"
---
# <a name="makecab"></a>makecab

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

キャビネット (.cab) ファイルに既存のファイルをパッケージ化します。


> [!NOTE]
> このコマンドは、コマンドと同じ[です。](diantz.md)

## <a name="syntax"></a>構文

```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<source>` | ファイルを圧縮します。 |
| `<destination>` | ファイル名を使用して、圧縮されたファイルに付けます。 省略すると、ソース ファイル名の最後の文字はアンダー スコア (_) に置き換えられ、送信先として使用します。 |
| /f `<directives_file>` | 持つファイル **makecab** ディレクティブ (繰り返し可能性があります)。 |
| /d var =`<value>` | 指定した値を含む変数を定義します。 |
| /l`<dir>` | 変換先を配置する場所 (既定値は現在のディレクトリ)。 |
| /v[`<n>`] | 詳細レベルのデバッグ設定 (0 = なし、..., 3 = フル)。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コマンドの実行 (z)](diantz.md)

- [Microsoft キャビネット形式](/previous-versions/bb417343(v=msdn.10))
