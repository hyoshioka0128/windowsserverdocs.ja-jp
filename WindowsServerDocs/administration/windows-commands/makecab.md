---
title: makecab
description: Makecab コマンドのリファレンストピックでは、既存のファイルをキャビネット (.cab) ファイルにパッケージ化します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 192471e6045a530e9deedec70cc957b9362b3ae7
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354662"
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コマンドの実行 (z)](diantz.md)

- [Microsoft キャビネット形式](https://docs.microsoft.com/previous-versions/bb417343(v=msdn.10))
