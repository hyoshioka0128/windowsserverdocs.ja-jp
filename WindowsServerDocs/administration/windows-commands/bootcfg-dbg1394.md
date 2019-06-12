---
title: bootcfg dbg1394
description: Windows コマンド」のトピック**bootcfg dbg1394** -指定したオペレーティング システム エントリの構成の 1394 ポートのデバッグ
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 85a554e25d1553ea4cd9415bb180df4751966926
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434844"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティング システム エントリの 1394 ポート デバッグを構成します。

## <a name="syntax"></a>構文
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
## <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                                                           説明                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   {ON &AMP;#124; OFF}    | 1394 ポートのデバッグの値を指定します。<br /><br />-   **ON** -リモート デバッグのサポートを指定した/dbg1394 オプションを追加することにより<OSEntryLineNum>します。<br />-   **オフ**-指定された対象から/dbg1394 オプションを削除することでリモート デバッグのサポートを無効にします<OSEntryLineNum>します。 |
|    /s <computer>     |                                                                                        名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                        |
| /u <Domain>\\<User>  |                                               指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。                                               |
|    /p <Password>     |                                                                                                      指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                       |
|     /ch チャネル      |                                                           デバッグに使用するチャネルを指定します。 有効な値は、1 ~ 64 の範囲の整数です。 使用しないでください、 **/ch** <Channel> 1394 ポートのデバッグを無効にされている場合は、パラメーター。                                                           |
| /id <OSEntryLineNum> |                                  1394 ポートのデバッグ オプションを追加する Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。                                  |
|          /?          |                                                                                                                               コマンド プロンプトにヘルプを表示します。                                                                                                                               |

## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/dbg1394**コマンド。
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)
