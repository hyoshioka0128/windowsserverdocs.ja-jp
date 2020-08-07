---
title: finger
description: 指のサービスまたはデーモンを実行している指定されたリモートコンピューター上のユーザーに関する情報を表示する、finger コマンドの参照記事です。
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 503b431905d764d371bff0c69eef9032fb0c8644
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890206"
---
# <a name="finger"></a>finger

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指サービスまたはデーモンを実行している、指定されたリモートコンピューター (通常は UNIX を実行しているコンピューター) 上のユーザーに関する情報を表示します。 リモートコンピューターは、ユーザー情報の表示形式と出力形式を指定します。 パラメーターを指定せずに使用すると、**指**でヘルプが表示されます。

> [!IMPORTANT]
> このコマンドは、インターネット プロトコル (TCP/IP) プロトコルがネットワーク接続のネットワーク アダプターのプロパティでコンポーネントとしてインストールされている場合にのみ使用できます。

## <a name="syntax"></a>構文

```
finger [-l] [<user>] [@<host>] [...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -l | 長い一覧形式でユーザー情報を表示します。 |
| `<user>` | 情報を必要とするユーザーを指定します。 *User*パラメーターを省略した場合、このコマンドは、指定されたコンピューター上のすべてのユーザーに関する情報を表示します。 |
| `@<host>` | ユーザー情報を探している finger サービスを実行しているリモートコンピューターを指定します。 コンピューター名または IP アドレスを指定できます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **指**パラメーターの前には、スラッシュ (/) ではなくハイフン (-) を付ける必要があります。

- 複数 `user@host` のパラメーターを指定できます。

### <a name="examples"></a>例

コンピューター *users.microsoft.com*に*user1*の情報を表示するには、次のように入力します。

```
finger user1@users.microsoft.com
```

コンピューター *users.microsoft.com*の*すべてのユーザー*の情報を表示するには、次のように入力します。

```
finger @users.microsoft.com
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
