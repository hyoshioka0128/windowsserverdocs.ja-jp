---
title: cmdkey
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc2b12cb53eef930d05c1e291de5574a8ba94306
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379310"
---
# <a name="cmdkey"></a>cmdkey

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

保存されたユーザー名とパスワードのほか、資格情報の作成、一覧表示、削除を行います。

## <a name="syntax"></a>構文
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
## <a name="parameters"></a>パラメーター

|             パラメーター             |                                                                                    説明                                                                                     |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /add: <TargetName>          | ユーザー名とパスワードを一覧に追加します。<br /><br />@No__t-0 のパラメーターが必要です。このパラメーターは、このエントリが関連付けられるコンピューターまたはドメイン名を識別します。 |
|       /汎用: <TargetName>        |   汎用的な資格情報をリストに追加します。<br /><br />@No__t-0 のパラメーターが必要です。このパラメーターは、このエントリが関連付けられるコンピューターまたはドメイン名を識別します。    |
|             /smartcard             |                                                                    スマートカードから資格情報を取得します。                                                                     |
|          /user: <UserName>          |                                 このエントリで格納するユーザー名またはアカウント名を指定します。 *UserName*が指定されていない場合は、要求されます。                                  |
|          /pass: <Password>          |                                       このエントリで格納するパスワードを指定します。 *パスワード*が指定されていない場合は、要求されます。                                        |
| /delete{: <TargetName> &#124; /ras} |  ユーザー名とパスワードを一覧から削除します。 *TargetName*を指定すると、そのエントリは削除されます。 /Ras を指定した場合、格納されているリモートアクセスエントリが削除されます。   |
|         /list: <TargetName>         |                  保存されているユーザー名と資格情報の一覧を表示します。 *TargetName*が指定されていない場合、保存されているすべてのユーザー名と資格情報が一覧表示されます。                   |
|                 /?                 |                                                                        コマンド プロンプトにヘルプを表示します。                                                                        |

## <a name="remarks"></a>コメント
- /smartcard コマンドラインオプションを使用しているときに、システムに複数のスマートカードが見つかった場合、使用可能なすべてのスマートカードに関する情報が表示され、使用するスマートカードを指定するように**求められ**ます。
- パスワードは、保存されると表示されません。
  ## <a name="BKMK_examples"></a>例
  保存されているすべてのユーザー名と資格情報の一覧を表示するには、次のように入力します。
  ```
  cmdkey /list
  ```
  パスワード Kleo でコンピューター Server01 にアクセスするためのユーザー名とパスワードを追加するには、次のように入力します。
  ```
  cmdkey /add:server01 /user:mikedan /pass:Kleo
  ```
  コンピューター Server01 にアクセスするためのユーザー名とパスワードを追加して、Server01 にアクセスするたびにパスワードの入力を求めるには、次のように入力します。
  ```
  cmdkey /add:server01 /user:mikedan
  ```
  リモートアクセスに格納されている資格情報を削除するには、次のように入力します。
  ```
  cmdkey /delete /ras
  ```
  Server01 に格納されている資格情報を削除するには、次のように入力します。
  ```
  cmdkey /delete:Server01
  ```
  ## <a name="additional-references"></a>その他の参照情報
  [コマンド ライン構文の記号](command-line-syntax-key.md)
