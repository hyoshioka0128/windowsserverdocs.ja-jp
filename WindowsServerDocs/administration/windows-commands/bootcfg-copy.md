---
title: bootcfg copy
description: Windows コマンド」のトピック**bootcfg コピー** -コマンド ライン オプションに追加することができます、既存のブート エントリのコピーを作成します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff8cf2751b229c6358e240444de940658f2eb2fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825513"
---
# <a name="bootcfg-copy"></a>bootcfg copy

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンド ライン オプションを追加することができます、既存のブート エントリのコピーを作成します。

## <a name="syntax"></a>構文
```
bootcfg /copy [/s <computer> [/u <Domain>\<User> /p <Password>]] [/d <Description>] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u <Domain>\\<User>|指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p <Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/d <Description>|新しいオペレーティング システム エントリの説明を指定します。|
|/id <OSEntryLineNum>|コピーする Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/copy** 1 のブート エントリをコピーしてコマンド"\ABC Server\\"説明として。
```
bootcfg /copy /d "\ABC Server\" /id 1
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
