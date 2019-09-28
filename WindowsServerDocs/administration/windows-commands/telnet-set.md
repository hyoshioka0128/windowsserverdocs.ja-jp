---
title: telnet セット
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e39e2812edc9cd5f169a046def26beebda1d007e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383621"
---
# <a name="telnet-set"></a>telnet: 設定

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オプションを設定します。   
## <a name="syntax"></a>構文  
```  
set [bsasdel] [crlf] [delasbs] [escape <Char>] [localecho] [logfile <FileName>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]  
```  
### <a name="parameters"></a>パラメーター  

|                    パラメーター                     |                                                                                                                                              説明                                                                                                                                              |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     bsasdel                      |                                                                                                                                 **Backspace**を**削除**として送信します。                                                                                                                                  |
|                       crlf                       |                                                                                                        CR、LF、(&) を送信 (0x0D、0x0a) と、 **Enter** キーが押されました。 改行モードとして知られています。                                                                                                        |
|                     delasbs                      |                                                                                                                                 **Delete**を**Backspace**として送信します。                                                                                                                                  |
|                エスケープ <Character>                | Telnet クライアントプロンプトを入力するために使用するエスケープ文字を設定します。 エスケープ文字、一文字でもかまいませんの組み合わせを使用して、 **ctrl キーを押し** さらに、文字キーです。 コントロール キーの組み合わせを設定するキーを押し、 **CTRL** を割り当てる必要がある文字を入力するときにキーします。 |
|                    localecho                     |                                                                                                                                         ローカル エコーをオンにします。                                                                                                                                          |
|                ログファイル <FileName>                |                                                                                               現在の telnet セッションをローカルファイルに記録します。 ログ記録は、このオプションを設定すると自動的に開始します。                                                                                               |
|                     logging                      |                                                                                                                  ログ記録を有効にします。 ログ ファイルが設定されていない場合、エラー メッセージが表示されます。                                                                                                                   |
|           {コンソールと &#124; 画面} モード           |                                                                                                                                       操作モードを設定します。                                                                                                                                        |
|                       ntlm                       |                                                                                                                                     NTLM 認証を有効にします。                                                                                                                                     |
| {ansi &#124; vt100 &#124; vt52 &#124; vtnt} 用語 |                                                                                                                                        端末の種類を設定します。                                                                                                                                        |
|                        ?                         |                                                                                                                                    このコマンドのヘルプを表示します。                                                                                                                                    |

## <a name="remarks"></a>注釈  
1. 使用することができます、 **未設定** コマンドに設定されているオプションをオフにします。  
2. 英語以外のバージョンの telnet では、**コードセット**<option> を使用できます。 **コードセット**<option> は、現在のコードセットをオプションに設定します。これは、次のいずれかになります: **shift JIS**、**日本語 EUC**、 **jis 漢字**、 **jis 漢字 (78)** 、 **DEC 漢字**、 **NEC 漢字**。 同じコードがリモート コンピューターのセットを設定する必要があります。  
   ## <a name="BKMK_Examples"></a>例  
   ログ ファイルを設定し、ローカル ファイル tnlog.txt へのログ記録を開始  
   ```  
   set logfile tnlog.txt  
   ```  
   ## <a name="additional-references"></a>その他の参照情報  
3. [コマンド ライン構文の記号](command-line-syntax-key.md)  
