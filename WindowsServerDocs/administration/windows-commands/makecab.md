---
title: makecab
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b120cf990abe2024fd6c96ca2f1ef11fa2350ae
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437533"
---
# <a name="makecab"></a>makecab

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

キャビネット (.cab) ファイルに既存のファイルをパッケージ化します。
## <a name="syntax"></a>構文
```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```
### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                        説明                                                                        |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|       <source>       |                                                                     ファイルを圧縮します。                                                                     |
|    <destination>     | ファイル名を使用して、圧縮されたファイルに付けます。 省略すると、ソース ファイル名の最後の文字はアンダー スコア (_) に置き換えられ、送信先として使用します。 |
| /f < directives_file > |                                                   持つファイル **makecab** ディレクティブ (繰り返し可能性があります)。                                                   |
|    /d var =<value>    |                                                          指定した値を含む変数を定義します。                                                           |
|       /l <dir>       |                                               変換先を配置する場所 (既定値は現在のディレクトリ)。                                               |
|       /v[<n>]        |                                                    詳細レベルのデバッグ設定 (0 = なし、..., 3 = フル)。                                                     |
|          /?          |                                                           コマンド プロンプトにヘルプを表示します。                                                            |

## <a name="remarks"></a>注釈
-   参照してください[Microsoft キャビネット形式](https://go.microsoft.com/fwlink/?LinkId=226852)ディレクティブ ・ ファイルについては msdn です。

## <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)

