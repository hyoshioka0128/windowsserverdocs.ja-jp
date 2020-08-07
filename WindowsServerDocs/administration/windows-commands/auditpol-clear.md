---
title: auditpol clear
description: Auditpol clear コマンドの参照記事。すべてのユーザーについてユーザーごとの監査ポリシーが削除され、すべてのサブカテゴリのシステム監査ポリシーがリセット (無効) され、すべての監査オプションが無効に設定されます。
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2cdb55633e15484f8ca98432fbe8bc28b5f59fd0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895453"
---
# <a name="auditpol-clear"></a>auditpol clear

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべてのユーザーのユーザーごとの監査ポリシーを削除し、すべてのサブカテゴリのシステム監査ポリシーをリセット (無効) し、すべての監査オプションを [無効] に設定します。

*ユーザーごと*のポリシーと*システム*ポリシーに対して*明確*な操作を実行するには、セキュリティ記述子でそのオブジェクトセットの**書き込み**または**フルコントロール**のアクセス許可を持っている必要があります。 **監査とセキュリティログの管理**(SeSecurityPrivilege) ユーザー権限を持っている場合は、*クリア*操作を実行することもできます。 ただし、この権限を使用すると、全体的な*クリア*操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="syntax"></a>構文

```
auditpol /clear [/y]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ----------- | --------------- |
| /y | すべての監査ポリシー設定をクリアする必要があるかどうかを確認するプロンプトを表示しません。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

すべてのユーザーのユーザーごとの監査ポリシーを削除するには、すべてのサブカテゴリのシステム監査ポリシーをリセット (無効) し、すべての監査ポリシー設定を無効に設定します。確認プロンプトで、次のように入力します。

```
auditpol /clear
```

すべてのユーザーのユーザーごとの監査ポリシーを削除するには、すべてのサブカテゴリのシステム監査ポリシー設定をリセットし、確認プロンプトを表示せずにすべての監査ポリシー設定を無効に設定して、次のように入力します。

```
auditpol /clear /y
```

> [!NOTE]
> 前の例は、スクリプトを使用してこの操作を実行する場合に役立ちます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [auditpol コマンド](auditpol.md)
