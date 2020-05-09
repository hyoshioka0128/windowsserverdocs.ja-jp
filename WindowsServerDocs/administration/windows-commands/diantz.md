---
title: diantz
description: 既存のファイルをキャビネット (.cab) ファイルにパッケージ化する、dipackages z コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 218ed5d7-1203-4d68-ad9b-65cdd022d54f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e45c0c4f71bc7faf6d5de0fa198ac872f6ff2597
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992503"
---
# <a name="diantz"></a>diantz

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

キャビネット (.cab) ファイルに既存のファイルをパッケージ化します。 このコマンドは、更新された[makecab コマンド](makecab.md)と同じ操作を実行します。

## <a name="syntax"></a>構文

```
diantz [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
diantz [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<source>` | ファイルを圧縮します。 |
| `<destination>` | ファイル名を使用して、圧縮されたファイルに付けます。 省略すると、ソース ファイル名の最後の文字はアンダー スコア (_) に置き換えられ、送信先として使用します。 |
| /f `<directives_file>` | (繰り返される場合もありますが **) 使用されているファイル**。 |
| /d var =`<value>` | 指定した値を含む変数を定義します。 |
| /l`<dir>` | 変換先を配置する場所 (既定値は現在のディレクトリ)。 |
| /v[`<n>`] | 詳細レベルのデバッグ設定 (0 = なし、..., 3 = フル)。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Microsoft キャビネット形式](https://docs.microsoft.com/previous-versions/bb417343(v=msdn.10))
