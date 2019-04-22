---
title: exit
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b3490c6bc95a762bf2cb1da70f389fb8f583344f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819493"
---
# <a name="exit"></a>exit

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Cmd.exe プログラム (コマンド インタープリター) または現在のバッチ スクリプトを終了します。  
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。  
## <a name="syntax"></a>構文  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|/b|Cmd.exe を終了せず、現在のバッチ スクリプトを終了します。 バッチ スクリプトの外から実行する場合は、Cmd.exe を終了します。|  
|<exitCode>|数値の数を指定します。 場合 **/b**を指定すると、ERRORLEVEL 環境変数は、その番号に設定されます。 終了が場合**Cmd.exe**、プロセス終了コードは、その番号に設定されます。|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="BKMK_examples"></a>例  
閉じるには、コマンド インタープリターを Cmd.exe、次のように入力します。  
```  
exit  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
