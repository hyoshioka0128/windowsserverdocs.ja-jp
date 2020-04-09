---
title: cmdkey
description: Windows コマンドに関するトピック。 cmdkey は、格納されているユーザー名とパスワードまたは資格情報を作成、一覧表示、および削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cdb732bf95e30af012f78d1bad337d6d6d191268
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847595"
---
# <a name="cmdkey"></a>cmdkey

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

保存されたユーザー名とパスワードのほか、資格情報の作成、一覧表示、削除を行います。

## <a name="syntax"></a>構文
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
### <a name="parameters"></a>パラメーター

|             パラメーター             |                                                                                    説明                                                                                     |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /add:<TargetName>          | ユーザー名とパスワードを一覧に追加します。<p>このエントリが関連付けられるコンピューターまたはドメイン名を識別する <TargetName> のパラメーターが必要です。 |
|       /汎用:<TargetName>        |   汎用的な資格情報をリストに追加します。<p>このエントリが関連付けられるコンピューターまたはドメイン名を識別する <TargetName> のパラメーターが必要です。    |
|             /smartcard             |                                                                    スマートカードから資格情報を取得します。                                                                     |
|          /user:<UserName>          |                                 このエントリで格納するユーザー名またはアカウント名を指定します。 *UserName*が指定されていない場合は、要求されます。                                  |
|          /pass:<Password>          |                                       このエントリで格納するパスワードを指定します。 *パスワード*が指定されていない場合は、要求されます。                                        |
| /delete{:<TargetName> &#124; /ras} |  ユーザー名とパスワードを一覧から削除します。 *TargetName*を指定すると、そのエントリは削除されます。 /Ras を指定した場合、格納されているリモートアクセスエントリが削除されます。   |
|         /list:<TargetName>         |                  保存されているユーザー名と資格情報の一覧を表示します。 *TargetName*が指定されていない場合、保存されているすべてのユーザー名と資格情報が一覧表示されます。                   |
|                 /?                 |                                                                        コマンド プロンプトでヘルプを表示します。                                                                        |

## <a name="remarks"></a>コメント
- /smartcard コマンドラインオプションを使用しているときに、システムに複数のスマートカードが見つかった場合、使用可能なすべてのスマートカードに関する情報が表示され、使用するスマートカードを指定するように**求められ**ます。
- パスワードは、保存されると表示されません。
  ## <a name="examples"></a><a name=BKMK_examples></a>例
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
  - [コマンド ライン構文の記号](command-line-syntax-key.md)
