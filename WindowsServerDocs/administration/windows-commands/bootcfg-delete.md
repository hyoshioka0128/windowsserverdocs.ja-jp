---
title: bootcfg delete
description: Bootcfg delete の Windows コマンドに関するトピックでは、Boot.ini ファイルのオペレーティングシステムセクションにあるオペレーティングシステムのエントリを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 71382e29-9b39-41c8-9c23-cf0ff829440a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01ec7a4dde1e22982f2cf0fa30245c33e09cc0ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848545"
---
# <a name="bootcfg-delete"></a>bootcfg delete

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini ファイルの [オペレーティングシステム] セクションにあるオペレーティングシステムのエントリを削除します。

## <a name="syntax"></a>構文
```
bootcfg /delete [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>パラメーター

|         用語         |                                                                                             Definition                                                                                              |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User>  | <User>または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
|    /p <Password>     |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                        |
| /id <OSEntryLineNum> |        削除する Boot.ini ファイルの [オペレーティングシステム] セクションにあるオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。        |
|          /?          |                                                                                コマンド プロンプトでヘルプを表示します。                                                                                 |

## <a name="examples"></a><a name=BKMK_examples></a>例
次の例は、 **bootcfg/delete**コマンドを使用する方法を示しています。
```
bootcfg /delete /id 1
bootcfg /delete /s srvmain /u maindom\hiropln /p p@ssW23 /id 3
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
