---
title: telnet セット
description: Telnet set の Windows コマンドに関するトピック。オプションを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8fefc18bde39713c3864361118ff4440ca12b0d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833165"
---
# <a name="telnet-set"></a>telnet: 設定

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オプションを設定します。   

## <a name="syntax"></a>構文  
```  
set [bsasdel] [crlf] [delasbs] [escape <Char>] [localecho] [logfile <FileName>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]  
```  
#### <a name="parameters"></a>パラメーター  

|                    パラメーター                     |                                                                                                                                              説明                                                                                                                                              |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     bsasdel                      |                                                                                                                                 **Backspace**を**削除**として送信します。                                                                                                                                  |
|                       crlf                       |                                                                                                        CR、LF、(&) を送信 (0x0D、0x0a) と、 **Enter** キーが押されました。 改行モードとして知られています。                                                                                                        |
|                     delasbs                      |                                                                                                                                 **Delete**を**Backspace**として送信します。                                                                                                                                  |
|                エスケープ <Character>                | Telnet クライアントプロンプトを入力するために使用するエスケープ文字を設定します。 エスケープ文字、一文字でもかまいませんの組み合わせを使用して、 **ctrl キーを押し** さらに、文字キーです。 コントロール キーの組み合わせを設定するキーを押し、 **CTRL** を割り当てる必要がある文字を入力するときにキーします。 |
|                    localecho                     |                                                                                                                                         ローカル エコーをオンにします。                                                                                                                                          |
|                ログファイルの <FileName>                |                                                                                               現在の telnet セッションをローカルファイルに記録します。 このオプションを設定すると、自動的にログの記録が開始されます。                                                                                               |
|                     ログ記録                      |                                                                                                                  ログ記録を有効にします。 ログ ファイルが設定されていない場合、エラー メッセージが表示されます。                                                                                                                   |
|           {コンソールと #124; 画面} モード           |                                                                                                                                       操作モードを設定します。                                                                                                                                        |
|                       ntlm                       |                                                                                                                                     NTLM 認証を有効にします。                                                                                                                                     |
| {ansi & #124; vt100 & #124; vt52 & #124; vtnt} 用語 |                                                                                                                                        端末の種類を設定します。                                                                                                                                        |
|                        ?                         |                                                                                                                                    このコマンドのヘルプを表示します。                                                                                                                                    |

## <a name="remarks"></a>コメント  
1. 使用することができます、 **未設定** コマンドに設定されているオプションをオフにします。  
2. 英語以外のバージョンの telnet では、**コードセット**<option> を使用できます。 **コードセット**<option> は、現在のコードセットをオプションに設定します。これには、次のいずれかを指定できます: **shift JIS**、**日本語 EUC**、 **jis 漢字**、 **jis 漢字 (78)** 、 **DEC 漢字**、 **NEC 漢字**。 同じコードがリモート コンピューターのセットを設定する必要があります。  
   ## <a name="examples"></a><a name=BKMK_Examples></a>例  
   ログ ファイルを設定し、ローカル ファイル tnlog.txt へのログ記録を開始  
   ```  
   set logfile tnlog.txt  
   ```  
   ## <a name="additional-references"></a>その他の参照情報  
3. - [コマンド ライン構文の記号](command-line-syntax-key.md)  
