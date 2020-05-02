---
title: exit
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e47dfa42f2bacb3fe9f12d1da9163bcf828e9488
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725704"
---
# <a name="exit"></a>exit

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Cmd.exe プログラム (コマンドインタープリター) または現在のバッチスクリプトを終了します。  
  
## <a name="syntax"></a>構文  
```  
exit [/b] [<exitCode>]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター  |                                                                                         [説明]                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Cmd.exe を終了する代わりに、現在のバッチスクリプトを終了します。 バッチスクリプトの外部から実行された場合は、Cmd.exe を終了します。                                      |
| `<exitCode>` | 数値を指定します。 **/B**が指定されている場合、ERRORLEVEL 環境変数はその数値に設定されます。 **Cmd.exe**を終了すると、プロセス終了コードはその番号に設定されます。 |
|     /?     |                                                                             コマンド プロンプトにヘルプを表示します。                                                                             |

## <a name="examples"></a>例  
コマンドインタープリター Cmd.exe を閉じるには、次のように入力します。  
```  
exit  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  

