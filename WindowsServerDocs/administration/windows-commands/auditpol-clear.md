---
title: auditpol クリア
description: '**Auditpol clear**の Windows コマンドに関するトピックでは、すべてのユーザーのユーザーごとの監査ポリシーを削除し、すべてのサブカテゴリのシステム監査ポリシーをリセット (無効) し、すべての監査オプションを無効に設定しています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 971f4ba54d787be29cb9e7d710f556c50c69a8dc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851205"
---
# <a name="auditpol-clear"></a>auditpol クリア

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべてのユーザーのユーザーごとの監査ポリシーを削除し、すべてのサブカテゴリのシステム監査ポリシーをリセット (無効) し、すべての監査オプションを [無効] に設定します。

## <a name="syntax"></a>構文

```
auditpol /clear [/y]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ----------- | --------------- |
| /y | すべての監査ポリシー設定をクリアする必要があるかどうかを確認するプロンプトを表示しません。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

ユーザーごとのポリシーとシステムポリシーの明確な操作を行うには、セキュリティ記述子で設定されたそのオブジェクトに対する書き込みまたはフルコントロールのアクセス許可が必要です。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を使用して、クリア操作を実行することもできます。 ただし、この権限を使用すると、クリア操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

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
