---
title: auditpol バックアップ
description: Windows コマンドの順序の**バックアップ**に関するトピックでは、システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、およびすべての監査オプションをコンマ区切り値 (CSV) テキストファイルにバックアップします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8895f312606a6a6c45a77c659a1cd98d115babe3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851215"
---
# <a name="auditpol-backup"></a>auditpol バックアップ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、およびすべての監査オプションをコンマ区切り値 (CSV) テキストファイルにバックアップします。

## <a name="syntax"></a>構文

```
auditpol /backup /file:<filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|-----------|------------- |
| /file | 監査ポリシーがバックアップされるファイルの名前を指定します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

ユーザーごとのポリシーとシステムポリシーのバックアップ操作については、セキュリティ記述子で設定されたそのオブジェクトに対する書き込みまたはフルコントロールのアクセス許可を持っている必要があります。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を使用して、バックアップ操作を実行することもできます。 ただし、この権限により、リスト操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

すべてのユーザー、システム監査ポリシー設定、およびすべての監査オプションのユーザーごとの監査ポリシー設定を、auditpolicy .csv という名前の CSV 形式のテキストファイルにバックアップするには、次のように入力します。

```
auditpol /backup /file:C:\auditpolicy.csv
```

> [!NOTE]
> ドライブが指定されていない場合は、現在のディレクトリが使用されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
- [auditpol 復元](auditpol-restore.md)
