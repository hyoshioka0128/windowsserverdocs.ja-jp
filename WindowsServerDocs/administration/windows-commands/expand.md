---
title: 展開
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ab4b9bcb5c9da2aeace71a8e535fa762d6d6e95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844875"
---
# <a name="expand"></a>展開

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1つ以上の圧縮ファイルを展開します。 このコマンドを使用して、配布ディスクから圧縮ファイルを取得できます。  
## <a name="syntax"></a>構文  
```  
expand [/r] <source> <destination>  
expand /r <source> [<destination>]  
expand /i <source> [<destination>]  
expand /d <source>.cab [/f:<files>]  
expand <source>.cab /f:<files> <destination>  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター  |                                                                                                                                                                   説明                                                                                                                                                                    |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /r      |                                                                                                                                                             展開されたファイルの名前を変更します。                                                                                                                                                              |
|   source    |                                                                              展開するファイルを指定します。 *ソース*は、ドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせで構成されます。 ワイルドカード ( **\\** \* または **?** ) を使用できます。                                                                               |
| 描画先 | ファイルの展開先を指定します。<p>*ソース*が複数のファイルで構成されていて、 **/r**を指定しない場合、 *destination*はディレクトリである必要があります。<p>*宛先*には、ドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせを使用できます。<p>ターゲットファイル&#124;パスの指定。 |
|     /i      |                                                                                                   展開されたファイルの名前を変更しますが、ディレクトリ構造は無視します。<p>このパラメーターは、Windows Server 2008 R2 と Windows 7 に適用されます。                                                                                                    |
|     /d      |                                                                                                                              展開元のファイル一覧を表示します。 ファイルの展開や抽出は行われません。                                                                                                                              |
|     /f:     |                                                                                                                 拡張するキャビネット (.cab) ファイル内のファイルを指定します。 ワイルドカード ( **\\** \* または **?** ) を使用できます。                                                                                                                 |
|     /?      |                                                                                                                                                       コマンド プロンプトでヘルプを表示します。                                                                                                                                                       |

## <a name="remarks"></a>コメント  
- 回復コンソールでの**展開**の使用  
  パラメーターが異なる**expand**コマンドは、回復コンソールから使用できます。 回復コンソールの詳細については、Microsoft サポート技術情報の[記事 314058](https://support.microsoft.com/kb/314058)を参照してください。  
  ## <a name="additional-references"></a>その他の参照情報  
  - [コマンド ライン構文の記号](command-line-syntax-key.md)  
