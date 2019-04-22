---
title: bootcfg default
description: Windows コマンド」のトピック**bootcfg 既定**-既定値として指定するオペレーティング システム エントリを指定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e21824d7-8278-41d7-a2c5-ce09803d513a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa19c787182584e941850bb38e6c4e8006790fca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823153"
---
# <a name="bootcfg-default"></a>bootcfg default

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定値として指定するオペレーティング システム エントリを指定します。

## <a name="syntax"></a>構文
```
bootcfg /default [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u <Domain>\\<User>|指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p <Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/id <OSEntryLineNum>|既定値として指定する Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/default**コマンド。
```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
