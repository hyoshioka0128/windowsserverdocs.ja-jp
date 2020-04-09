---
title: bootcfg default
description: 既定値として指定するオペレーティングシステムエントリを指定する、bootcfg default の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e21824d7-8278-41d7-a2c5-ce09803d513a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 517cf444a5517b3d612266b57b428e47ac60d4ef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848566"
---
# <a name="bootcfg-default"></a>bootcfg default

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定値として指定するオペレーティングシステムエントリを指定します。

## <a name="syntax"></a>構文
```
bootcfg /default [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                             説明                                                                                              |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                          名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User>  | <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
|    /p <Password>     |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                         |
| /id <OSEntryLineNum> | Boot.ini ファイルの [オペレーティングシステム] セクションで、既定として指定するオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。  |
|          /?          |                                                                                 コマンド プロンプトでヘルプを表示します。                                                                                 |

## <a name="examples"></a><a name=BKMK_examples></a>例
次の例は、 **bootcfg/default**コマンドを使用する方法を示しています。
```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
