---
title: auditpol オフ
description: Windows コマンド」のトピック**auditpol オフ**-すべてのユーザー、リセット (無効)、システム監査ポリシー サブカテゴリ、およびすべての監査を無効にオプション セットのすべてのユーザーごとの監査ポリシーを削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 453579589f3fd3cc2c9fa835b50bfb59e33bc3dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872583"
---
# <a name="auditpol-clear"></a>auditpol オフ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべてのユーザー、リセット (無効)、システム監査ポリシー サブカテゴリ、およびすべての監査を無効にオプション セットのすべてのユーザーごとの監査ポリシーを削除します。

## <a name="syntax"></a>構文
```
auditpol /clear [/y]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/y|すべての監査ポリシーの設定をクリアするかどうかの確認メッセージを抑制します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
ユーザーごとのポリシーおよびシステム ポリシーのクリア操作で、記述する必要がありますがまたはそのオブジェクトに対するフル コントロール権限がセキュリティ記述子に設定します。 所有することによって、消去操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、消去操作を実行する必要はありません、追加のアクセスを許可します。
## <a name="BKMK_examples"></a>例
すべてのユーザー、リセット (無効) のすべてのサブカテゴリ システム監査ポリシーを設定がすべてのユーザーごとの監査ポリシーを削除するには、監査ポリシーの設定を無効に、確認プロンプトに入力します。
```
auditpol /clear
```
すべてのユーザーのユーザーごとの監査ポリシーを削除するには、サブカテゴリのすべてのシステム監査ポリシーの設定をリセットし、すべての監査ポリシー設定を無効な場合、確認プロンプトで、入力せずに設定。
```
auditpol /clear /y
```
> [!NOTE]
> 前の例は、この操作を実行するスクリプトを使用する場合に便利です。
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
