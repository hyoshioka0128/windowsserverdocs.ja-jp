---
title: bootcfg addsw
description: Windows コマンド」のトピック**bootcfg addsw** -オペレーティング システムの読み込みオプションの指定したオペレーティング システム エントリを追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 768e9c5bcf8a5d272927d013ff4accf5c3237219
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862873"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オペレーティング システムの読み込みオプションの指定したオペレーティング システム エントリを追加します。

## <a name="syntax"></a>構文
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
## <a name="parameters"></a>パラメーター
|用語|定義|
|----|-------|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u <Domain>\\<User>|指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p <Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/mm <MaximumRAM>|オペレーティング システムが使用できるメガバイト単位で、RAM の最大量を指定します。 値は、32 メガバイト以上である必要があります。|
|/bv|追加、 **/basevideo**を指定したオプション<OSEntryLineNum>にインストールされているビデオ ドライバーの標準の VGA モードを使用するオペレーティング システムに指示します。|
|/so|追加、 **/sos**を指定したオプション*OSEntryLineNum*、読み込み中には、デバイス ドライバーの名前を表示するオペレーティング システムに指示します。|
|/ng|追加、**選択する**を指定したオプション<OSEntryLineNum>CTRL + ALT + del ログオンする前にプロンプトに表示される進行状況バーを無効にするとします。|
|/id <OSEntryLineNum>|オペレーティング システムの読み込みオプションを追加する Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/addsw**コマンド。
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
