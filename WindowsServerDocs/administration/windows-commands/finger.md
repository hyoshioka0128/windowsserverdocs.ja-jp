---
title: finger
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78313fc4980b32e3aeb6d1611ef80d7eb6831fc1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844605"
---
# <a name="finger"></a>finger

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指サービスまたはデーモンを実行している、指定されたリモートコンピューター (通常は UNIX を実行しているコンピューター) 上のユーザーに関する情報を表示します。 リモートコンピューターは、ユーザー情報の表示形式と出力形式を指定します。 パラメーターを指定せずに使用すると、**指**でヘルプが表示されます。 
## <a name="syntax"></a>構文
```
finger [-l] [<User>] [@<Host>] [...]
```
#### <a name="parameters"></a>パラメーター

| パラメーター |                                                                            説明                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          長い一覧形式でユーザー情報を表示します。                                                           |
|  <User>   | 情報を必要とするユーザーを指定します。 *User*パラメーターを省略すると、**指**を使用すると、指定したコンピューター上のすべてのユーザーに関する情報が表示されます。 |
|  @<Host>  |        ユーザー情報を探している finger サービスを実行しているリモートコンピューターを指定します。 コンピューター名または IP アドレスを指定できます。        |
|    /?     |                                                               コマンド プロンプトでヘルプを表示します。                                                                |

## <a name="remarks"></a>コメント
複数の User@Host パラメーターを指定できます。
**指**パラメーターの前には、スラッシュ (/) ではなくハイフン (-) を付ける必要があります。
このコマンドは、インターネット プロトコル (TCP/IP) プロトコルがネットワーク接続のネットワーク アダプターのプロパティでコンポーネントとしてインストールされている場合にのみ使用できます。
Windows Server 2003 では、finger サービスは提供されていません。
## <a name="examples"></a><a name=BKMK_Examples></a>例
コンピューター users.microsoft.com に user1 の情報を表示するには、次のように入力します。
```
finger user1@users.microsoft.com
```
コンピューター users.microsoft.com のすべてのユーザーの情報を表示するには、次のように入力します。
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
