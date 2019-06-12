---
title: bootcfg rmsw
description: Windows コマンド」のトピック**bootcfg rmsw** - オペレーティング システムの読み込みオプションの指定したオペレーティング システム エントリを削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3d873cffbdb386b5f4f564801a4f4b815c6987a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434680"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オペレーティング システムの読み込みオプションの指定したオペレーティング システム エントリを削除します。

## <a name="syntax"></a>構文
```
bootcfg /rmsw [/s <computer> [/u <Domain>\<User> [/p <Password>]]] [/mm] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
## <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                      説明                                                                                                       |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                   名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                   |
| /u <Domain>\\<User>  |          指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。          |
|    /p <Password>     |                                                                 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                  |
|         /mm          |           指定された対象から/maxmem オプションとその関連付けられているメモリの最大値を削除します。<OSEntryLineNum>します。 /Maxmem オプションでは、オペレーティング システムが使用できる RAM の最大量を指定します。            |
|         /bv          |                     指定された対象から/basevideo オプションを削除します。<OSEntryLineNum>します。 /Basevideo オプションは、インストールされているビデオ ドライバーの標準の VGA モードを使用するオペレーティング システムに指示します。                     |
|         /so          |                         指定された対象から/sos オプションを削除します。<OSEntryLineNum>します。 /Sos オプションは、読み込み中には、デバイス ドライバーの名前を表示するオペレーティング システムに指示します。                          |
|         /ng          |                         指定された対象から選択するオプションを削除します。<OSEntryLineNum>します。 選択するオプションには、CTRL + ALT + del ログオン プロンプトの前に表示される進行状況バーが無効にします。                          |
| /id <OSEntryLineNum> | OS の読み込みオプションの削除元となる、Boot.ini ファイルの [オペレーティング システム] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。 |
|          /?          |                                                                                          コマンド プロンプトにヘルプを表示します。                                                                                          |

## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/rmsw**コマンド。
```
bootcfg /rmsw /mm 64 /id 2 
bootcfg /rmsw /so /id 3 
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /rmsw /ng /id 2 
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2       
```
#### <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)
