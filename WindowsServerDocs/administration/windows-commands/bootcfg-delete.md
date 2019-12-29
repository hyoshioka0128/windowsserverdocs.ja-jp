---
title: bootcfg delete
description: '**Bootcfg の削除**に関する Windows コマンドのトピックでは、boot.ini ファイルのオペレーティングシステムセクションにあるオペレーティングシステムエントリが削除されます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71382e29-9b39-41c8-9c23-cf0ff829440a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d2298c07af32e66a2ffcebb85ec780da762be58
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380009"
---
# <a name="bootcfg-delete"></a>bootcfg delete

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

boot.ini ファイルの [オペレーティングシステム] セクションにあるオペレーティングシステムのエントリを削除します。

## <a name="syntax"></a>構文
```
bootcfg /delete [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター

|         用語         |                                                                                             定義                                                                                              |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User>  | <User>または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
|    /p <Password>     |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                        |
| /id <OSEntryLineNum> |        削除する Boot.ini ファイルの [オペレーティングシステム] セクションにあるオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。        |
|          /?          |                                                                                コマンド プロンプトにヘルプを表示します。                                                                                 |

## <a name="BKMK_examples"></a>例
次の例は、 **bootcfg/delete**コマンドを使用する方法を示しています。
```
bootcfg /delete /id 1
bootcfg /delete /s srvmain /u maindom\hiropln /p p@ssW23 /id 3
```
#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
