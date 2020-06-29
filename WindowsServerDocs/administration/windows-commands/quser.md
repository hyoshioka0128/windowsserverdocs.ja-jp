---
title: quser
description: リモートデスクトップセッションホストサーバー上のユーザーセッションに関する情報を表示する、quser コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8056204f-ed11-4c91-bb1d-c799283a48a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e51abe030ca0f473246cdc85fd01d89fddf8b056
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471927"
---
# <a name="quser"></a>quser

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホストサーバー上のユーザーセッションに関する情報を表示します。 このコマンドを使用すると、特定のユーザーが特定のリモートデスクトップセッションホストサーバーにログオンしているかどうかを確認できます。 このコマンドは、次の情報を返します。

- ユーザーの名前

- リモートデスクトップセッションホストサーバー上のセッションの名前

- セッション ID

- セッションの状態 (アクティブまたは切断)

- アイドル時間 (セッションで最後のキーストロークまたはマウスの移動からの分数)

- ユーザーがログオンした日付と時刻

> [!NOTE]
> このコマンドは、 [query user コマンド](query-user.md)と同じです。 最新バージョンの新機能については、「 [Windows Server でのリモートデスクトップサービスの新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))機能」を参照してください。

## <a name="syntax"></a>構文

```
quser [<username> | <sessionname> | <sessionID>] [/server:<servername>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<username>` | クエリを実行するユーザーのログオン名を指定します。 |
| `<sessionname>` | クエリを実行するセッションの名前を指定します。 |
| `<sessionID>` | クエリを実行するセッションの ID を指定します。 |
| /server:`<servername>` | クエリを実行するリモートデスクトップセッションホストサーバーを指定します。 それ以外の場合は、現在のリモートデスクトップセッションホストサーバーが使用されます。 このパラメーターは、リモートサーバーからこのコマンドを使用している場合にのみ必要です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- このコマンドを使用するには、フルコントロールアクセス許可または特殊なアクセス許可が必要です。

- <*username*> *、<の*sessionID>、または*sessionID*パラメーターを使用してユーザーを指定しない場合、サーバーにログオンしているすべてのユーザーの一覧が返されます。 または、 **query session**コマンドを使用して、サーバー上のすべてのセッションの一覧を表示することもできます。

- **Quser**が情報を返すと、 `(>)` 現在のセッションの前に不等号が表示されます。

### <a name="examples"></a>例

システムにログオンしているすべてのユーザーに関する情報を表示するには、次のように入力します。

```
quser
```

サーバー *Server1*のユーザー *USER1*に関する情報を表示するには、次のように入力します。

```
quser USER1 /server:Server1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [クエリユーザーコマンド](query-user.md)

- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
