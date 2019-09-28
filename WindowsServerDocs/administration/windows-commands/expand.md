---
title: expand
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4a88222ffe9ff374626a6406c330a6660d992f96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377319"
---
# <a name="expand"></a>expand

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1つ以上の圧縮ファイルを展開します。 このコマンドを使用して、配布ディスクから圧縮ファイルを取得できます。  
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
|   source    |                                                                              展開するファイルを指定します。 *ソース*は、ドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせで構成されます。 ワイルドカード ( **\\** \* または **?** ) を使用できます。                                                                               |
| 変換先 (destination) | ファイルを展開する場所を指定します。<br /><br />*ソース*が複数のファイルで構成されていて、 **/r**を指定しない場合、 *destination*はディレクトリである必要があります。<br /><br />*宛先*には、ドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせを使用できます。<br /><br />ターゲットファイル&#124;パスの指定。 |
|     /i      |                                                                                                   展開されたファイルの名前を変更しますが、ディレクトリ構造は無視します。<br /><br />このパラメーターは、次のものに適用されます。Windows Server 2008 R2 および Windows 7。                                                                                                    |
|     /d      |                                                                                                                              ソースの場所にあるファイルの一覧を表示します。 では、ファイルの展開や抽出は行われません。                                                                                                                              |
|     /f:     |                                                                                                                 拡張するキャビネット (.cab) ファイル内のファイルを指定します。 ワイルドカード ( **\\** \* または **?** ) を使用できます。                                                                                                                 |
|     /?      |                                                                                                                                                       コマンド プロンプトにヘルプを表示します。                                                                                                                                                       |

## <a name="remarks"></a>コメント  
- 回復コンソールでの**展開**の使用  
  パラメーターが異なる**expand**コマンドは、回復コンソールから使用できます。 回復コンソールの詳細については、Microsoft サポート技術情報の[記事 314058](https://support.microsoft.com/kb/314058)を参照してください。  
  ## <a name="additional-references"></a>その他の参照情報  
  [コマンド ライン構文の記号](command-line-syntax-key.md)  
