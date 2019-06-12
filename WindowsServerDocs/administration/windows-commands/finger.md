---
title: finger
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 526363db3ecff4a9138c9cf13cbf330196e14ced
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439253"
---
# <a name="finger"></a>finger

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

本の指のサービスまたはデーモンが実行されている指定されたリモート コンピューター (通常は UNIX を実行しているコンピューター) 上のユーザーまたはユーザーに関する情報を表示します。 リモート コンピューターには、書式設定とユーザー情報の表示の出力を指定します。 パラメーターを指定せずに使用される**指**ヘルプを表示します。 
## <a name="syntax"></a>構文
```
finger [-l] [<User>] [@<Host>] [...]
```
### <a name="parameters"></a>パラメーター

| パラメーター |                                                                            説明                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          長いリスト形式でユーザー情報を表示します。                                                           |
|  <User>   | 情報を表示ユーザーを指定します。 省略した場合、*ユーザー*パラメーター、**指**指定したコンピューター上のすべてのユーザーに関する情報を表示します。 |
|  @<Host>  |        ユーザー情報を調べる本の指のサービスを実行するリモート コンピューターを指定します。 コンピューター名または IP アドレスを指定することができます。        |
|    /?     |                                                               コマンド プロンプトにヘルプを表示します。                                                                |

## <a name="remarks"></a>注釈
複数User@Hostパラメーターを指定することができます。
プレフィックスにする必要があります**指**スラッシュ (/) ではなくハイフン (-) を持つパラメーター。
このコマンドは、インターネット プロトコル (TCP/IP) プロトコルがネットワーク接続のネットワーク アダプターのプロパティでコンポーネントとしてインストールされている場合にのみ使用できます。
Windows Server 2003 では、本の指のサービスは提供されません。
## <a name="BKMK_Examples"></a>例
をコンピューター users.microsoft.com 上 user1 の情報を表示するには、次のように入力します。
```
finger user1@users.microsoft.com
```
をコンピューター users.microsoft.com 上のすべてのユーザーの情報を表示するには、次のように入力します。
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
