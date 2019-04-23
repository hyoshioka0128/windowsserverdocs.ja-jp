---
title: auditpol 復元
description: Windows コマンド」のトピック**auditpol 復元**-システム監査ポリシーの設定、ユーザーごとの監査ポリシーの設定、すべてのユーザーとすべての監査オプションをコンマ区切りで構文的に一貫性のあるファイルから復元します。/backup で使用される値 (CSV) ファイル形式オプション。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad73e520-484f-4cf1-a7f9-ae7488e9edf6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1961387083a8a61b27f3e44a2380a6060a02f98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868983"
---
# <a name="auditpol-restore"></a>auditpol 復元

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム監査ポリシーの設定、すべてのユーザーとすべての監査オプションをユーザーごとの監査ポリシーの設定を/backup で使用されるコンマ区切り値 (CSV) ファイル形式と構文的に一貫性のあるファイルから復元するオプション。

## <a name="syntax"></a>構文
```
auditpol /restore /file:<filename>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/file|監査ポリシーの復元元ファイルを指定します。 ファイルを/backup を使用して作成する必要がありますオプションや、/backup で使用される CSV ファイル形式と構文的に一致する必要がありますオプション。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
ユーザーごとのポリシーおよびシステム ポリシーの復元操作を記述する必要がありますがまたはセキュリティ記述子でそのオブジェクトに対するフル コントロール アクセス許可を設定します。 所有することによって、復元操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 SeSecurityPrivilege、不注意によるエラーや悪意のある攻撃が発生した場合、セキュリティ記述子を復元するときに便利です。
## <a name="BKMK_examples"></a>例
システム監査ポリシーの設定、すべてのユーザーとすべての監査オプションをユーザーごとの監査ポリシーの設定を/backup を使用して作成された auditpolicy.csv という名前のファイルから復元するコマンドを入力します。
```
auditpol /restore /file:c:\auditpolicy.csv
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[auditpol バックアップ](auditpol-backup.md)
