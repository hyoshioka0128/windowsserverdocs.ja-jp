---
title: bootcfg addsw
description: Bootcfg addsw の Windows コマンドに関するトピックでは、指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9ae5175dfc3b068276f6ab95d6823699c96b2b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848715"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加します。

## <a name="syntax"></a>構文
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
### <a name="parameters"></a>パラメーター

|         用語         |                                                                                                            Definition                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                        名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                        |
| /u <Domain>\\<User>  |               <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。               |
|    /p <Password>     |                                                                      指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                       |
|   /mm <MaximumRAM>   |                                          オペレーティングシステムが使用できる RAM の最大容量を mb 単位で指定します。 値は 32 Mb 以上である必要があります。                                          |
|         /bv          |                                    指定された <OSEntryLineNum>に **/basevideo**オプションを追加し、インストールされているビデオドライバーの標準 VGA モードを使用するようにオペレーティングシステムに指示します。                                     |
|         /so          |                                      指定された*OSEntryLineNum*に **/sos**オプションを追加し、読み込み中にデバイスドライバー名を表示するようにオペレーティングシステムに指示します。                                      |
|         /ng          |                                         指定された <OSEntryLineNum>に **/noguiboot**オプションを追加し、CTRL + ALT + del ログオンプロンプトの前に表示される進行状況バーを無効にします。                                          |
| /id <OSEntryLineNum> | オペレーティングシステムの読み込みオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
|          /?          |                                                                                               コマンド プロンプトでヘルプを表示します。                                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>例
次の例は、 **bootcfg/addsw**コマンドを使用する方法を示しています。
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
