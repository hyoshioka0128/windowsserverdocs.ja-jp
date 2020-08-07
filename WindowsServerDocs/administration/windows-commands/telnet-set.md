---
title: telnet set
description: オプションを設定する telnet set のリファレンス記事です。
ms.topic: article
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2cfc3daaa882effbea0c8dba6471ceeee1216681
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881668"
---
# <a name="telnet-set"></a>telnet: 設定

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
|                付ける<Character>                | Telnet クライアントプロンプトを入力するために使用するエスケープ文字を設定します。 エスケープ文字、一文字でもかまいませんの組み合わせを使用して、 **ctrl キーを押し** さらに、文字キーです。 コントロール キーの組み合わせを設定するキーを押し、 **CTRL** を割り当てる必要がある文字を入力するときにキーします。 |
|                    localecho                     |                                                                                                                                         ローカル エコーをオンにします。                                                                                                                                          |
|                ログファイル<FileName>                |                                                                                               現在の telnet セッションをローカルファイルに記録します。 ログ記録は、このオプションを設定すると自動的に開始します。                                                                                               |
|                     logging                      |                                                                                                                  ログ記録を有効にします。 ログ ファイルが設定されていない場合、エラー メッセージが表示されます。                                                                                                                   |
|           {コンソールと #124; 画面} モード           |                                                                                                                                       操作モードを設定します。                                                                                                                                        |
|                       ntlm                       |                                                                                                                                     NTLM 認証を有効にします。                                                                                                                                     |
| {ansi & #124; vt100 & #124; vt52 & #124; vtnt} 用語 |                                                                                                                                        端末の種類を設定します。                                                                                                                                        |
|                        ?                         |                                                                                                                                    このコマンドのヘルプを表示します。                                                                                                                                    |

## <a name="remarks"></a>Remarks
1. 使用することができます、 **未設定** コマンドに設定されているオプションをオフにします。
2. 英語以外のバージョンの telnet では、**コードセット**を <option> 使用できます。 **コードセット** <option>現在のコードセットをオプションに設定します。これには、次のいずれかを指定できます: **SHIFT JIS**、**日本語 EUC**、 **jis 漢字**、 **Jis 漢字 (78)**、 **DEC 漢字**、 **NEC 漢字**。 同じコードがリモート コンピューターのセットを設定する必要があります。
   ## <a name="examples"></a>例
   ログ ファイルを設定し、ローカル ファイル tnlog.txt へのログ記録を開始
   ```
   set logfile tnlog.txt
   ```
   ## <a name="additional-references"></a>その他の参照情報
3. - [コマンド ライン構文の記号](command-line-syntax-key.md)
