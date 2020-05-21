---
title: eventcreate
description: Eventcreate コマンドのリファレンストピック。これにより、管理者は、指定されたイベントログにカスタムイベントを作成できます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8348e61f6cd94c9b660d0ad9cac4cb1f96920cad
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436877"
---
# <a name="eventcreate"></a>eventcreate

管理者が、指定されたイベントログにカスタムイベントを作成できるようにします。

> [!IMPORTANT]
> カスタムイベントをセキュリティログに書き込むことはできません。

## <a name="syntax"></a>構文

```
eventcreate [/s <computer> [/u <domain\user> [/p <password>]] {[/l {APPLICATION|SYSTEM}]|[/so <srcname>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <eventID> /d <description>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| /s`<computer>` | 名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。 |
| /u`<domain\user>` | またはによって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行し `<user>` `<domain\user>` ます。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| /p`<password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| /l`{APPLICATION | SYSTEM}` | イベントが作成されるイベントログの名前を指定します。 有効なログ名は、**アプリケーション**または**システム**です。 |
| /so`<srcname>` | イベントに使用するソースを指定します。 有効なソースは任意の文字列にすることができ、イベントを生成しているアプリケーションまたはコンポーネントを表す必要があります。 |
| /t`{ERROR | WARNING | INFORMATION | SUCCESSAUDIT | FAILUREAUDIT}` | 作成するイベントの種類を指定します。 有効な種類は、 **ERROR**、 **WARNING**、 **INFORMATION**、 **SUCCESSAUDIT**、および**failureaudit**です。 |
| /id`<eventID>` | イベントのイベント ID を指定します。 有効な ID は、1 ~ 1000 の任意の数です。 |
| d`<description>` | 新しく作成されたイベントに使用する説明を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

次の例は、 **eventcreate**コマンドを使用する方法を示しています。

```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
