---
title: exit
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13cf7a7658394e59ce6cc7e66c3083cd3d359574
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844885"
---
# <a name="exit"></a>exit

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Cmd.exe プログラム (コマンドインタープリター) または現在のバッチスクリプトを終了します。  
このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。  
## <a name="syntax"></a>構文  
```  
exit [/b] [<exitCode>]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター  |                                                                                         説明                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Cmd.exe を終了する代わりに、現在のバッチスクリプトを終了します。 バッチスクリプトの外部から実行された場合は、Cmd.exe を終了します。                                      |
| `<exitCode>` | 数値を指定します。 **/B**が指定されている場合、ERRORLEVEL 環境変数はその数値に設定されます。 **Cmd.exe**を終了すると、プロセス終了コードはその番号に設定されます。 |
|     /?     |                                                                             コマンド プロンプトでヘルプを表示します。                                                                             |

## <a name="examples"></a><a name=BKMK_examples></a>例  
コマンドインタープリター Cmd.exe を閉じるには、次のように入力します。  
```  
exit  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  

