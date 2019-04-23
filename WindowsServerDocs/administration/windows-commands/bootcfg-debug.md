---
title: bootcfg debug
description: Windows コマンド」のトピック**bootcfg デバッグ**- を追加または指定したオペレーティング システム エントリのデバッグ設定を変更します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27768788e7f14445137331523c62151fcf3b6b2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879023"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

追加または指定したオペレーティング システム エントリのデバッグ設定を変更します。

## <a name="syntax"></a>構文
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|{ON &#124; OFF&#124;編集}|デバッグの値を指定します。<br /><br />**ON** -リモート デバッグのサポートを指定した、/debug オプションを追加することにより<OSEntryLineNum>します。<br /><br />**オフ**-指定された対象から、/debug オプションを削除することでリモート デバッグのサポートを無効にします<OSEntryLineNum>します。<br /><br />**編集**-により、指定された、/debug オプションに関連付けられている値を変更することで、ポートとボーへの変更の頻度の設定<OSEntryLineNum>します。|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u <Domain>\\<User>|指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p <Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|ポート {COM1 &#124; COM2 &#124; COM3 &#124; COM4}|デバッグに使用する COM ポートを指定します。 使用しないでください、 **/port**デバッグする場合は、パラメーターが無効にします。|
|/baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200}|デバッグに使用するボー レートを指定します。 使用しないでください、 **/baud**デバッグする場合は、パラメーターが無効にします。|
|/id <OSEntryLineNum>|デバッグ オプションを追加する Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。|
|/?|コマンド プロンプトにヘルプを表示します。|
##### <a name="remarks"></a>注釈
-   1394 ポートのデバッグが必要な場合は、使用[bootcfg dbg1394](bootcfg-dbg1394.md)します。
## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/debug**コマンド。
```
bootcfg /debug on /port com1 /id 2 
bootcfg /debug edit /port com2 /baud 19200 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
