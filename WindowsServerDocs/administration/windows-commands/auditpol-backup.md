---
title: auditpol バックアップ
description: '**Auditpol バックアップ**の Windows コマンドトピック-システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、およびすべての監査オプションをコンマ区切り値 (CSV) テキストファイルにバックアップします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 96b98a05740d3ce1bfe14eda4c5d97ba6c09ff32
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382451"
---
# <a name="auditpol-backup"></a>auditpol バックアップ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、およびすべての監査オプションをコンマ区切り値 (CSV) テキストファイルにバックアップします。

## <a name="syntax"></a>構文
```
auditpol /backup /file:<filename>
```
## <a name="parameters"></a>パラメーター

| パラメーター |                                 説明                                 |
|-----------|-----------------------------------------------------------------------------|
|   /file   | 監査ポリシーがバックアップされるファイルの名前を指定します。 |
|    /?     |                    コマンド プロンプトにヘルプを表示します。                     |

## <a name="remarks"></a>コメント
ユーザーごとのポリシーとシステムポリシーのバックアップ操作については、セキュリティ記述子で設定されたそのオブジェクトに対する書き込みまたはフルコントロールのアクセス許可を持っている必要があります。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を使用して、バックアップ操作を実行することもできます。 ただし、この権限により、リスト操作を実行するために必要な追加のアクセス権が許可されます。
## <a name="BKMK_examples"></a>例
すべてのユーザー、システム監査ポリシー設定、およびすべての監査オプションのユーザーごとの監査ポリシー設定を、auditpolicy .csv という名前の CSV 形式のテキストファイルにバックアップするには、次のように入力します。
```
auditpol /backup /file:C:\auditpolicy.csv 
```
> [!NOTE]
> ドライブが指定されていない場合は、現在のディレクトリが使用されます。
> #### <a name="additional-references"></a>その他の参照情報
> [コマンドライン構文のキー](command-line-syntax-key.md)
> [auditpol 復元](auditpol-restore.md)
