---
title: bootcfg dbg1394
description: '**Bootcfg dbg1394**の Windows コマンドのトピック-指定したオペレーティングシステムエントリに対して1394ポートのデバッグを構成する'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8550871c60343fdc6d797f3f81729c24270400b4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380088"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたオペレーティングシステムエントリに対して1394ポートデバッグを構成します。

## <a name="syntax"></a>構文
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
## <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                                                           説明                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   {ON &#124; OFF}    | 1394ポートデバッグの値を指定します。<br /><br />-   **ON** -指定した <OSEntryLineNum>に/dbg1394 オプションを追加することにより、リモートデバッグのサポートを有効にします。<br />-   **OFF** -指定された <OSEntryLineNum>から/dbg1394 オプションを削除することによって、リモートデバッグのサポートを無効にします。 |
|    /s <computer>     |                                                                                        名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                        |
| /u <Domain>\\<User>  |                                               <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。                                               |
|    /p <Password>     |                                                                                                      指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                       |
|     /ch チャネル      |                                                           デバッグに使用するチャネルを指定します。 有効な値は、1 ~ 64 の整数です。 1394ポートデバッグが無効になっている場合は、 **/ch** <Channel> パラメーターを使用しないでください。                                                           |
| /id <OSEntryLineNum> |                                  1394ポートデバッグオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。                                  |
|          /?          |                                                                                                                               コマンド プロンプトにヘルプを表示します。                                                                                                                               |

## <a name="BKMK_examples"></a>例
次の例は、 **bootcfg/dbg1394**コマンドを使用する方法を示しています。
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
