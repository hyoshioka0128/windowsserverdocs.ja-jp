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
ms.openlocfilehash: 63aaa7a044634d29c61f3085b1f0c015f4e64444
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434833"
---
# <a name="bootcfg-default"></a>bootcfg default

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定値として指定するオペレーティング システム エントリを指定します。

## <a name="syntax"></a>構文
```
bootcfg /default [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                             説明                                                                                              |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                          名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User>  | 指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。 |
|    /p <Password>     |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                         |
| /id <OSEntryLineNum> | 既定値として指定する Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。  |
|          /?          |                                                                                 コマンド プロンプトにヘルプを表示します。                                                                                 |

## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/default**コマンド。
```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)
