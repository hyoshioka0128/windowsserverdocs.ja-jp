---
title: auditpol の削除
description: Windows コマンド」のトピック**auditpol 削除**-指定されたアカウントまたはすべてのアカウントのユーザーごとの監査ポリシーを削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be42ec55-235c-44f7-9abd-ed1cf3f5b1f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 566827e93d9f8c9dc0d00f4f704513369fbb44ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818303"
---
# <a name="auditpol-remove"></a>auditpol の削除

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたアカウントまたはすべてのアカウントのユーザーごとの監査ポリシーを削除します。

## <a name="syntax"></a>構文
```
auditpol /remove [/user[:<username>|<{SID}>]]
[/allusers]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/user|セキュリティ識別子 (SID) を指定します。 または、対象のユーザーごとの監査ポリシーのユーザーのユーザー名を削除するのには。|
|/allusers|すべてのユーザーのユーザーごとの監査ポリシーを削除します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
ユーザーごとのポリシーの削除操作で、そのオブジェクトのセキュリティ記述子の設定で書き込みまたはフル コントロール権限が必要です。 所有することによって、削除操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、削除操作を実行する必要はありません、追加のアクセスを許可します。
## <a name="BKMK_examples"></a>例
名前によってユーザー mikedan のユーザーごとの監査ポリシーを削除するに次のように入力します。
```
auditpol /remove /user:mikedan
```
SID によって mikedan をユーザーのユーザーごとの監査ポリシーを削除するには、次のように入力します。
```
auditpol /remove /user:{S-1-5-21-397123471-12346959}
```
すべてのユーザーのユーザーごとの監査ポリシーを削除するには、次のように入力します。
```
auditpol /remove /allusers
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
