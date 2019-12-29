---
title: finger
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e16120eb19ff2f194fe2c8bdeb3af80ca459ebe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377163"
---
# <a name="finger"></a>finger

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指サービスまたはデーモンを実行している、指定されたリモートコンピューター (通常は UNIX を実行しているコンピューター) 上のユーザーに関する情報を表示します。 リモートコンピューターは、ユーザー情報の表示形式と出力形式を指定します。 パラメーターを指定せずに使用すると、**指**でヘルプが表示されます。 
## <a name="syntax"></a>構文
```
finger [-l] [<User>] [@<Host>] [...]
```
### <a name="parameters"></a>パラメーター

| パラメーター |                                                                            説明                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          長い一覧形式でユーザー情報を表示します。                                                           |
|  <User>   | 情報を必要とするユーザーを指定します。 *User*パラメーターを省略すると、**指**を使用すると、指定したコンピューター上のすべてのユーザーに関する情報が表示されます。 |
|  @<Host>  |        ユーザー情報を探している finger サービスを実行しているリモートコンピューターを指定します。 コンピューター名または IP アドレスを指定できます。        |
|    /?     |                                                               コマンド プロンプトにヘルプを表示します。                                                                |

## <a name="remarks"></a>コメント
複数の User@Host パラメーターを指定できます。
**指**パラメーターの前には、スラッシュ (/) ではなくハイフン (-) を付ける必要があります。
このコマンドは、インターネット プロトコル (TCP/IP) プロトコルがネットワーク接続のネットワーク アダプターのプロパティでコンポーネントとしてインストールされている場合にのみ使用できます。
Windows Server 2003 では、finger サービスは提供されていません。
## <a name="BKMK_Examples"></a>例
コンピューター users.microsoft.com に user1 の情報を表示するには、次のように入力します。
```
finger user1@users.microsoft.com
```
コンピューター users.microsoft.com のすべてのユーザーの情報を表示するには、次のように入力します。
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
