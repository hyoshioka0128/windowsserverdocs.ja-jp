---
title: makecab
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a0bf4afda09f0e0e8416777a2cfd1404d4bf59a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724219"
---
# <a name="makecab"></a>makecab

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

キャビネット (.cab) ファイルに既存のファイルをパッケージ化します。
## <a name="syntax"></a>構文
```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```
#### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                        [説明]                                                                        |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|       <source>       |                                                                     ファイルを圧縮します。                                                                     |
|    <destination>     | ファイル名を使用して、圧縮されたファイルに付けます。 省略すると、ソース ファイル名の最後の文字はアンダー スコア (_) に置き換えられ、送信先として使用します。 |
| /f < directives_file > |                                                   持つファイル **makecab** ディレクティブ (繰り返し可能性があります)。                                                   |
|    /d var =<value>    |                                                          指定した値を含む変数を定義します。                                                           |
|       /l<dir>       |                                               変換先を配置する場所 (既定値は現在のディレクトリ)。                                               |
|       /v[<n>]        |                                                    詳細レベルのデバッグ設定 (0 = なし、..., 3 = フル)。                                                     |
|          /?          |                                                           コマンド プロンプトにヘルプを表示します。                                                            |

## <a name="remarks"></a>Remarks
-   Directive_file の詳細については、MSDN の「 [Microsoft キャビネット形式](https://go.microsoft.com/fwlink/?LinkId=226852)」を参照してください。

## <a name="additional-references"></a>その他のリファレンス
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

