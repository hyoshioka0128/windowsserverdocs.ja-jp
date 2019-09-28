---
title: getmac
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c770f5da5159e0037af479f90fadb4cd83464c77
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375809"
---
# <a name="getmac"></a>getmac

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカルまたはネットワーク経由で、各コンピューターのすべてのネットワークカードの各アドレスに関連付けられている、メディアアクセス制御 (MAC) アドレスとネットワークプロトコルの一覧を返します。 
## <a name="syntax"></a>構文
```
getmac[.exe][/s <computer> [/u <Domain\<User> [/p <Password>]]][/fo {TABLE | list | CSV}][/nh][/v]
```
### <a name="parameters"></a>パラメーター

|             パラメーター              |                                                                                          説明                                                                                          |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s <computer>            |                                      名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                       |
|        /u <Domain> @ no__t @ no__t         | ユーザーまたは Domain\user によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
|           /p <Password>            |                                                     指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                     |
| /fo {テーブル&#124;一覧&#124;の CSV} |                       クエリ出力に使用する形式を指定します。 有効な値は、 **TABLE**、 **List**、および**CSV**です。 出力の既定の形式は**TABLE**です。                        |
|                /nh                 |                                             出力に列ヘッダーを表示しません。 **/Fo**パラメーターが**TABLE**または**CSV**に設定されている場合に有効です。                                              |
|                 /v                 |                                                                    出力に詳細情報を表示するように指定します。                                                                     |
|                 /?                 |                                                                                                                                                                                               |

## <a name="remarks"></a>コメント
**getmac**は、MAC アドレスをネットワークアナライザーに入力する場合や、コンピューターの各ネットワークアダプターで現在使用されているプロトコルを知る必要がある場合に役立ちます。
## <a name="BKMK_Examples"></a>例
次の例は、 **getmac**コマンドを使用する方法を示しています。
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
## <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
