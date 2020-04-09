---
title: bootcfg dbg1394
description: Bootcfg dbg1394 の Windows コマンドに関するトピックでは、指定されたオペレーティングシステムエントリに対して1394ポートのデバッグが構成されています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d49e0a39cd021f093ca68bf97963dc35c3b53ad4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848675"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたオペレーティングシステムエントリに対して1394ポートデバッグを構成します。

## <a name="syntax"></a>構文
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                                                           説明                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   {ON &#124; OFF}    | 1394ポートデバッグの値を指定します。<p>-   **ON** -指定した <OSEntryLineNum>に/dbg1394 オプションを追加することにより、リモートデバッグのサポートを有効にします。<br />-   **OFF** -指定された <OSEntryLineNum>から/dbg1394 オプションを削除することによって、リモートデバッグのサポートを無効にします。 |
|    /s <computer>     |                                                                                        名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                        |
| /u <Domain>\\<User>  |                                               <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。                                               |
|    /p <Password>     |                                                                                                      指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                       |
|     /ch チャネル      |                                                           デバッグに使用するチャネルを指定します。 有効な値は、1 ~ 64 の整数です。 1394ポートデバッグが無効になっている場合は、 **/ch** <Channel> パラメーターを使用しないでください。                                                           |
| /id <OSEntryLineNum> |                                  1394ポートデバッグオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。                                  |
|          /?          |                                                                                                                               コマンド プロンプトでヘルプを表示します。                                                                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>例
次の例は、 **bootcfg/dbg1394**コマンドを使用する方法を示しています。
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
