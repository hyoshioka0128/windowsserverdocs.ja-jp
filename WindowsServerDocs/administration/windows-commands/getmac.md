---
title: getmac
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a749a348-7cd1-4336-9f33-bb42dd0e31e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1266b7368f1b073e00735a8d3362c75305d7c0f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438268"
---
# <a name="getmac"></a>getmac

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

メディアを返します。 へのアクセス制御 (MAC) アドレス、またはネットワーク経由でに関連付けられている各コンピューターでは、すべてのネットワーク カードの各アドレスか、ローカル ネットワーク プロトコルの一覧。 
## <a name="syntax"></a>構文
```
getmac[.exe][/s <computer> [/u <Domain\<User> [/p <Password>]]][/fo {TABLE | list | CSV}][/nh][/v]
```
### <a name="parameters"></a>パラメーター

|             パラメーター              |                                                                                          説明                                                                                          |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s <computer>            |                                      名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                       |
|        /u <Domain>\\<User>         | ユーザーまたはドメイン \ ユーザーによって指定されたユーザーのアカウント権限でコマンドを実行します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。 |
|           /p <Password>            |                                                     指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                     |
| /fo {テーブル&#124;一覧&#124;CSV} |                       クエリ出力に使用する形式を指定します。 有効な値は**テーブル**、**一覧**、および**CSV**します。 出力の既定の形式は**テーブル**します。                        |
|                /nh                 |                                             出力の列ヘッダーを抑制します。 有効な場合に、 **/fo**にパラメーターが設定されている**テーブル**または**CSV**します。                                              |
|                 /v                 |                                                                    出力の詳細な情報を表示することを指定します。                                                                     |
|                 /?                 |                                                                                                                                                                                               |

## <a name="remarks"></a>注釈
**getmac**ネットワーク アナライザーに MAC アドレスを入力するとき、またはプロトコルは現在、コンピューターの場合は、各ネットワーク アダプター上で使用を把握する必要があるときに役に立ちます。
## <a name="BKMK_Examples"></a>例
次の例を使用する方法、 **getmac**コマンド。
```
getmac /fo table /nh /v
```
```
getmac /s srvmain
```
```
getmac /s srvmain /u maindom\hiropln
```
```
getmac /s srvmain /u maindom\hiropln /p p@ssW23
```
```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo list /v
```
```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo table /nh
```
## <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
