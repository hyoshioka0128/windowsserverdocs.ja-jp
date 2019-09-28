---
title: auditpol クリア
description: '**Auditpol**の Windows コマンドトピックでは、すべてのユーザーのユーザーごとの監査ポリシーを削除し、すべてのサブカテゴリのシステム監査ポリシーをリセット (無効) し、すべての監査オプションを無効に設定します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4fd2cce2b860ee41725b698dcd36ca38b2c4c6a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382417"
---
# <a name="auditpol-clear"></a>auditpol クリア

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべてのユーザーのユーザーごとの監査ポリシーを削除し、すべてのサブカテゴリのシステム監査ポリシーをリセット (無効) し、すべての監査オプションを [無効] に設定します。

## <a name="syntax"></a>構文
```
auditpol /clear [/y]
```
## <a name="parameters"></a>パラメーター

| パラメーター |                                   説明                                    |
|-----------|----------------------------------------------------------------------------------|
|    /y     | すべての監査ポリシー設定をクリアする必要があるかどうかを確認するプロンプトを表示しません。 |
|    /?     |                       コマンド プロンプトにヘルプを表示します。                       |

## <a name="remarks"></a>コメント
ユーザーごとのポリシーとシステムポリシーの明確な操作を行うには、セキュリティ記述子で設定されたそのオブジェクトに対する書き込みまたはフルコントロールのアクセス許可が必要です。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を使用して、クリア操作を実行することもできます。 ただし、この権限を使用すると、クリア操作を実行するために必要な追加のアクセス権が許可されます。
## <a name="BKMK_examples"></a>例
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
> #### <a name="additional-references"></a>その他の参照情報
> [コマンド ライン構文の記号](command-line-syntax-key.md)
