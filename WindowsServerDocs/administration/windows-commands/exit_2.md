---
title: exit
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 105bf572c1ebeb37ea59ff8bc5c04121d2442341
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377349"
---
# <a name="exit"></a>exit

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Cmd.exe プログラム (コマンドインタープリター) または現在のバッチスクリプトを終了します。  
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。  
## <a name="syntax"></a>構文  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>パラメーター  

| パラメーター  |                                                                                         説明                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Cmd.exe を終了する代わりに、現在のバッチスクリプトを終了します。 バッチスクリプトの外部から実行された場合は、Cmd.exe を終了します。                                      |
| <exitCode> | 数値を指定します。 **/B**が指定されている場合、ERRORLEVEL 環境変数はその数値に設定されます。 **Cmd.exe**を終了すると、プロセス終了コードはその番号に設定されます。 |
|     /?     |                                                                             コマンド プロンプトにヘルプを表示します。                                                                             |

## <a name="BKMK_examples"></a>例  
コマンドインタープリター Cmd.exe を閉じるには、次のように入力します。  
```  
exit  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  

