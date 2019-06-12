---
title: auditpol バックアップ
description: Windows コマンド」のトピック**auditpol バックアップ**-バックアップを作成するシステム監査ポリシーの設定]、[すべてのユーザーとすべての監査オプションをコンマ区切り値 (CSV) テキスト ファイルをユーザーごとの監査ポリシーの設定。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7de5e6dc6d205b7e6749d38ac822e31a78788c6e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435212"
---
# <a name="auditpol-backup"></a>auditpol バックアップ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

バックアップを作成するシステムでは、ポリシーの設定]、[すべてのユーザーとすべての監査オプションをコンマ区切り値 (CSV) テキスト ファイルをユーザーごとの監査ポリシーの設定を監査します。

## <a name="syntax"></a>構文
```
auditpol /backup /file:<filename>
```
## <a name="parameters"></a>パラメーター

| パラメーター |                                 説明                                 |
|-----------|-----------------------------------------------------------------------------|
|   /file   | 監査ポリシーのバックアップ先ファイルの名前を指定します。 |
|    /?     |                    コマンド プロンプトにヘルプを表示します。                     |

## <a name="remarks"></a>注釈
ユーザーごとのポリシーおよびシステム ポリシーのバックアップ操作を記述する必要がありますがまたはセキュリティ記述子でそのオブジェクトに対するフル コントロール アクセス許可を設定します。 所有することによって、バックアップ操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、リスト操作を実行する必要はありません、追加のアクセスを許可します。
## <a name="BKMK_examples"></a>例
ユーザーごとの監査をバックアップするには、すべてのユーザー、システムのポリシー設定の監査ポリシーの設定、および auditpolicy.csv、型をという名前の CSV 形式のテキスト ファイルにすべての監査オプション。
```
auditpol /backup /file:C:\auditpolicy.csv 
```
> [!NOTE]
> ドライブが指定されていない場合は、現在のディレクトリが使用されます。
> #### <a name="additional-references"></a>その他の参照
> [コマンドライン構文のポイント](command-line-syntax-key.md)
> [auditpol 復元](auditpol-restore.md)
