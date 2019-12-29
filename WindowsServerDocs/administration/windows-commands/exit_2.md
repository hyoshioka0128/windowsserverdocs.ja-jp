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
ms.openlocfilehash: d6d3a4d0bfc74644f6fda43abe57e0e4e7c1264a
ms.sourcegitcommit: 4a03f263952c993dfdf339dd3491c73719854aba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74791232"
---
# <a name="exit"></a>exit

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Cmd.exe プログラム (コマンドインタープリター) または現在のバッチスクリプトを終了します。  
このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。  
## <a name="syntax"></a>構文  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>パラメーター  

| パラメーター  |                                                                                         説明                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Cmd.exe を終了する代わりに、現在のバッチスクリプトを終了します。 バッチスクリプトの外部から実行された場合は、Cmd.exe を終了します。                                      |
| `<exitCode>` | 数値を指定します。 **/B**が指定されている場合、ERRORLEVEL 環境変数はその数値に設定されます。 **Cmd.exe**を終了すると、プロセス終了コードはその番号に設定されます。 |
|     /?     |                                                                             コマンド プロンプトにヘルプを表示します。                                                                             |

## <a name="BKMK_examples"></a>例  
コマンドインタープリター Cmd.exe を閉じるには、次のように入力します。  
```  
exit  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  

