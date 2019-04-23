---
title: bootcfg ems
description: Windows コマンド」のトピック**bootcfg ems** -ユーザーを追加またはリモート コンピューターに、緊急管理サービス コンソールのリダイレクトの設定を変更できます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57abdc50-c64a-45f1-8470-3f8c3a51f743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97f0126fdfa4d800692a044d33e3de0f0d4c6cdb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861643"
---
# <a name="bootcfg-ems"></a>bootcfg ems

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ユーザーを追加またはリモート コンピューターに、緊急管理サービス コンソールのリダイレクトの設定を変更できます。 緊急管理サービスを有効にして追加することを"リダイレクト ポート番号 ="Boot.ini ファイルおよび/redirect オプションの指定したオペレーティング システム エントリの行の [ブート ローダー] セクションに行。 緊急管理サービス機能は、サーバー上でのみ有効です。

## <a name="syntax"></a>構文
```
bootcfg /ems {ON | OFF | edit} [/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|{ON &#124; OFF&#124;編集}|緊急管理サービスのリダイレクトの値を指定します。<br /><br />**ON** -指定したリモートの出力を有効に<OSEntryLineNum>します。 指定した/redirect オプションが追加<OSEntryLineNum>とリダイレクト com を =<X> [ブート ローダー] セクションに設定します。 Com の値<X>で設定されて、 **/port**パラメーター。<br /><br />**オフ**-リモート コンピューターへの出力を無効にします。 指定された対象から/redirect オプションを削除します。<OSEntryLineNum>とリダイレクト com を =<X> [ブート ローダー] セクションから設定します。<br /><br />**編集**-リダイレクトを変更することでポート設定の変更は、com を =<X> [ブート ローダー] セクションで設定します。 Com の値<X>で指定された値にリセットされます、 **/port**パラメーター。|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u <Domain>\\<User>|指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p <Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/port {COM1 &#124; COM2 &#124; COM3 &#124; COM4 &#124; BIOSSET}|リダイレクトに使用する COM ポートを指定します。 **BIOSSET**リダイレクトにどのポートを使用する必要がありますを決定する BIOS 設定を取得する緊急管理サービスに指示します。 使用しないでください、 **/port**出力をリモートで管理される場合は、パラメーターが無効にします。|
|/baud {9600 &#124; 19200 &#124; 38400&#124; 57600 &#124; 115200}|リダイレクトに使用するボー レートを指定します。 使用しないでください、 **/baud**出力をリモートで管理される場合は、パラメーターが無効にします。|
|/id <OSEntryLineNum>|Boot.ini ファイルの [オペレーティング システム] セクションでは、緊急管理サービス オプションを追加するオペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。 緊急管理サービスの値に設定されている場合は、このパラメーターは必要**ON**または**OFF**します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/ems**コマンド。
```
bootcfg /ems on /port com1 /baud 19200 /id 2 
bootcfg /ems on /port biosset /id 3 
bootcfg /s srvmain /ems off /id 2 
bootcfg /ems edit /port com2 /baud 115200 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /ems off /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
