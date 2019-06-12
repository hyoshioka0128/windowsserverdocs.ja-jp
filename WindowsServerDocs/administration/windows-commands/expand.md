---
title: expand
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84fd3693ab41780f7092d74228a06503f9bca74f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439389"
---
# <a name="expand"></a>expand

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1 つまたは複数の圧縮されたファイルを展開します。 このコマンドを使用すると、パッケージ内のディスクから圧縮されたファイルを取得します。  
## <a name="syntax"></a>構文  
```  
expand [/r] <source> <destination>  
expand /r <source> [<destination>]  
expand /i <source> [<destination>]  
expand /d <source>.cab [/f:<files>]  
expand <source>.cab /f:<files> <destination>  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター  |                                                                                                                                                                   説明                                                                                                                                                                    |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /r      |                                                                                                                                                             展開されたファイルの名前を変更します。                                                                                                                                                              |
|   source    |                                                                              展開するファイルを指定します。 *ソース*のドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせで構成できます。 ワイルドカードを使用することができます ( **\\** \*または **?** )。                                                                               |
| 変換先 (destination) | ファイルの展開を指定します。<br /><br />場合*ソース*は複数のファイルを指定しないと **/r**、*先*ディレクトリである必要があります。<br /><br />*移行先*のドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせで構成できます。<br /><br />コピー先ファイル&#124;パスを指定します。 |
|     /i      |                                                                                                   展開されたファイルの名前を変更しますが、ディレクトリ構造は無視されます。<br /><br />このパラメーターに適用されます。Windows Server 2008 R2 および Windows 7。                                                                                                    |
|     /d      |                                                                                                                              ソースの場所にファイルの一覧を表示します。 展開またはファイルを展開しません。                                                                                                                              |
|     /f:     |                                                                                                                 キャビネット (.cab) ファイルを展開するには、ファイルを指定します。 ワイルドカードを使用することができます ( **\\** \*または **?** )。                                                                                                                 |
|     /?      |                                                                                                                                                       コマンド プロンプトにヘルプを表示します。                                                                                                                                                       |

## <a name="remarks"></a>注釈  
- 使用して**展開**回復コンソール  
  **展開**コマンドで他のパラメーターは、回復コンソールから利用できます。 回復コンソールの詳細については、次を参照してください。[記事 314058](https://support.microsoft.com/kb/314058)マイクロソフト サポート技術情報でします。  
  ## <a name="additional-references"></a>その他の参照  
  [コマンド ライン構文の記号](command-line-syntax-key.md)  
