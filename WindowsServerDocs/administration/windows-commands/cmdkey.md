---
title: cmdkey
description: 保存されているユーザー名とパスワードまたは資格情報を作成、一覧表示、削除する、cmdkey コマンドの参照記事です。
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7194b19231209150197fbc4c20175b319da77cd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880062"
---
# <a name="cmdkey"></a>cmdkey

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

保存されたユーザー名とパスワードのほか、資格情報の作成、一覧表示、削除を行います。

## <a name="syntax"></a>構文

```
cmdkey [{/add:<targetname>|/generic:<targetname>}] {/smartcard | /user:<username> [/pass:<password>]} [/delete{:<targetname> | /ras}] /list:<targetname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| /add`<targetname>` | ユーザー名とパスワードを一覧に追加します。<p>には、 `<targetname>` このエントリが関連付けられるコンピューターまたはドメイン名を識別するのパラメーターが必要です。 |
| /一般`<targetname>` | 汎用的な資格情報をリストに追加します。<p>には、 `<targetname>` このエントリが関連付けられるコンピューターまたはドメイン名を識別するのパラメーターが必要です。 |
| /smartcard | スマートカードから資格情報を取得します。 このオプションを使用したときにシステムに複数のスマートカードが見つかった場合、 **cmdkey**は使用可能なすべてのスマートカードに関する情報を表示し、使用するスマートカードを指定するようにユーザーに求めます。 |
| /user`<username>` | このエントリで格納するユーザー名またはアカウント名を指定します。 が指定されていない場合は `<username>` 、要求されます。 |
|渡す`<password>` | このエントリで格納するパスワードを指定します。 が指定されていない場合は `<password>` 、要求されます。 パスワードは、保存された後は表示されません。 |
| /delete{:`<targetname>` | 電話帳 | ユーザー名とパスワードを一覧から削除します。 `<targetname>`が指定されている場合、そのエントリは削除されます。 を指定した場合 `/ras` 、格納されているリモートアクセスエントリは削除されます。 |
| /list`<targetname>` | 保存されているユーザー名と資格情報の一覧を表示します。 が `<targetname>` 指定されていない場合は、保存されているユーザー名と資格情報がすべて一覧表示されます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

保存されているすべてのユーザー名と資格情報の一覧を表示するには、次のように入力します。

```
cmdkey /list
```

パスワード*Kleo*でコンピューター *Server01* *にアクセスするため*のユーザー名とパスワードを追加するには、次のように入力します。

```
cmdkey /add:server01 /user:mikedan /pass:Kleo
```

コンピューター *Server01* *にアクセスするため*のユーザー名とパスワードを追加して、Server01 にアクセスするたびにパスワードの入力を求めるには、次のように入力します。

```
cmdkey /add:server01 /user:mikedan
```

リモートアクセスによって格納された資格情報を削除するには、次のように入力します。

```
cmdkey /delete /ras
```

*Server01*に格納されている資格情報を削除するには、次のように入力します。

```
cmdkey /delete:server01
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
