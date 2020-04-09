---
title: auditpol の削除
description: '**Auditpol remove**に関する Windows コマンドのトピックでは、指定されたアカウントまたはすべてのアカウントのユーザーごとの監査ポリシーが削除されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be42ec55-235c-44f7-9abd-ed1cf3f5b1f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eda43d6708a31b2966022d2ae2c162bbfc888cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851175"
---
# <a name="auditpol-remove"></a>auditpol の削除

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたアカウントまたはすべてのアカウントについて、ユーザーごとの監査ポリシーを削除します。

## <a name="syntax"></a>構文

```
auditpol /remove [/user[:<username>|<{SID}>]]
[/allusers]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| /user | ユーザーごとの監査ポリシーを削除するユーザーのセキュリティ識別子 (SID) またはユーザー名を指定します。 |
| /allusers | すべてのユーザーのユーザーごとの監査ポリシーを削除します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

ユーザーごとのポリシーの削除操作については、セキュリティ記述子で設定されたオブジェクトに対する書き込みまたはフルコントロールのアクセス許可が必要です。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を所有して、削除操作を実行することもできます。 ただし、この権限により、削除操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

ユーザーごとのユーザーごとの監査ポリシーを名前で削除するには、次のように入力します。

```
auditpol /remove /user:mikedan
```

SID を使用して、ユーザーごとのユーザーごとの監査ポリシーを削除するには、次のように入力します。

```
auditpol /remove /user:{S-1-5-21-397123471-12346959}
```

すべてのユーザーのユーザーごとの監査ポリシーを削除するには、次のように入力します。

```
auditpol /remove /allusers
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
