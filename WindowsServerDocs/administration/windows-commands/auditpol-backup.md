---
title: auditpol backup
description: Auditpol backup コマンドの参照記事。このコマンドは、システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、およびすべての監査オプションをコンマ区切り値 (CSV) テキストファイルにバックアップします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8678dbc80b664e3ab667f197f708fbbdbbe40dc7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923811"
---
# <a name="auditpol-backup"></a>auditpol backup

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、およびすべての監査オプションをコンマ区切り値 (CSV) テキストファイルにバックアップします。

*ユーザーごと*のポリシーと*システム*ポリシーで*バックアップ*操作を実行するには、セキュリティ記述子でそのオブジェクトセットに対する**書き込み**または**フルコントロール**のアクセス許可が必要です。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利がある場合は、*バックアップ*操作を実行することもできます。 ただし、この権限では、*バックアップ*操作全体を実行するために必要な追加のアクセス権が許可されます。

## <a name="syntax"></a>構文

```
auditpol /backup /file:<filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|-----------|------------- |
| /file | 監査ポリシーがバックアップされるファイルの名前を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

すべてのユーザー、システム監査ポリシー設定、およびすべての監査オプションのユーザーごとの監査ポリシー設定を、auditpolicy.csv という名前の CSV 形式のテキストファイルにバックアップするには、次のように入力します。

```
auditpol /backup /file:C:\auditpolicy.csv
```

> [!NOTE]
> ドライブが指定されていない場合は、現在のディレクトリが使用されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [auditpol restore](auditpol-restore.md)

- [auditpol コマンド](auditpol.md)
