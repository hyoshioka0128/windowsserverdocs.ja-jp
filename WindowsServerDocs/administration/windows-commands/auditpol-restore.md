---
title: auditpol 復元
description: '**Auditpol 復元**の Windows コマンドトピック-システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、および/backup オプションで使用されるコンマ区切り値 (CSV) ファイル形式と構文的に一致するファイルからのすべての監査オプションを復元します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b91f3745354c695c4ab0c71b429718bff05d8098
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382411"
---
# <a name="auditpol-restore"></a>auditpol 復元

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、および/backup オプションで使用されるコンマ区切り値 (CSV) ファイル形式と構文的に一致するファイルからのすべての監査オプションを復元します。

## <a name="syntax"></a>構文
```
auditpol /restore /file:<filename>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/file|監査ポリシーの復元元のファイルを指定します。 このファイルは、/backup オプションを使用して作成されているか、/backup オプションで使用される CSV ファイル形式と構文的に一致している必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
ユーザーごとのポリシーとシステムポリシーの復元操作では、セキュリティ記述子でそのオブジェクトセットの書き込みまたはフルコントロールのアクセス許可を持っている必要があります。 また、 **[監査とセキュリティログの管理]** (SeSecurityPrivilege) ユーザー権利を使用して復元操作を実行することもできます。 SeSecurityPrivilege は、不注意なエラーや悪意のある攻撃が発生した場合にセキュリティ記述子を復元するときに役立ちます。
## <a name="BKMK_examples"></a>例
システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、および/backup コマンドを使用して作成された auditpolicy .csv という名前のファイルのすべての監査オプションを復元するには、次のように入力します。
```
auditpol /restore /file:c:\auditpolicy.csv
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[auditpol バックアップ](auditpol-backup.md)
