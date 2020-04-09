---
title: bootcfg rmsw
description: Bootcfg rmsw の Windows コマンドに関するトピックでは、指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションが削除されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 956732f396e0fa353a8acd55953e46605a5c4200
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848445"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを削除します。

## <a name="syntax"></a>構文
```
bootcfg /rmsw [/s <computer> [/u <Domain>\<User> [/p <Password>]]] [/mm] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                      説明                                                                                                       |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                   名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                   |
| /u <Domain>\\<User>  |          <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。          |
|    /p <Password>     |                                                                 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                  |
|         /mm          |           /maxmem オプションとそれに関連付けられている最大メモリ値を、指定した <OSEntryLineNum>から削除します。 /Maxmem オプションは、オペレーティングシステムが使用できる RAM の最大量を指定します。            |
|         /bv          |                     指定された <OSEntryLineNum>から/basevideo オプションを削除します。 /Basevideo オプションは、インストールされているビデオドライバーの標準 VGA モードを使用するようにオペレーティングシステムに指示します。                     |
|         /so          |                         指定された <OSEntryLineNum>から/sos オプションを削除します。 /Sos オプションは、ドライバーの読み込み中にデバイスドライバー名を表示するようにオペレーティングシステムに指示します。                          |
|         /ng          |                         指定した <OSEntryLineNum>から/noguiboot オプションを削除します。 /Noguiboot オプションを指定すると、CTRL + ALT + del ログオンプロンプトの前に表示される進行状況バーが無効になります。                          |
| /id <OSEntryLineNum> | ブート .ini ファイルの [オペレーティングシステム] セクションで、OS の読み込みオプションを削除するオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
|          /?          |                                                                                          コマンド プロンプトでヘルプを表示します。                                                                                          |

## <a name="examples"></a><a name=BKMK_examples></a>例
次の例は、 **bootcfg/rmsw**コマンドを使用する方法を示しています。
```
bootcfg /rmsw /mm 64 /id 2 
bootcfg /rmsw /so /id 3 
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /rmsw /ng /id 2 
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2       
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
