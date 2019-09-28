---
title: auditpol
description: '**Auditpol**の Windows コマンドのトピック-監査ポリシーを操作するための情報を表示し、関数を実行します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e249a9e2a07505f052b774208c514b4d16879b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382379"
---
# <a name="auditpol"></a>auditpol



に関する情報を表示し、監査ポリシーを操作する関数を実行します。

このコマンドを使用する方法の例については、各トピックの「例」を参照してください。

## <a name="syntax"></a>構文

```
Auditpol command [<sub-command><options>]
```

## <a name="parameters"></a>パラメーター

|サブコマンド|説明|
|-----------|-----------|
|/get|現在の監査ポリシーを表示します。</br>構文とオプションについては、「 [Auditpol get](auditpol-get.md) 」を参照してください。|
|/set|監査ポリシーを設定します。</br>構文とオプションについては、 [Auditpol の設定](auditpol-set.md)を参照してください。|
|/list|選択可能なポリシー要素を表示します。</br>構文とオプションについては、 [Auditpol の一覧](auditpol-list.md)を参照してください。|
|/backup|監査ポリシーをファイルに保存します。</br>構文とオプションについては、「 [Auditpol バックアップ](auditpol-backup.md)」を参照してください。|
|/restore|Auditpol/backupを使用して以前に作成されたファイルから監査ポリシーを復元します。</br>構文とオプションについては、 [Auditpol の復元](auditpol-restore.md)を参照してください。|
|/clear|監査ポリシーをクリアします。</br>構文とオプションについては、「 [Auditpol clear](auditpol-clear.md) 」を参照してください。|
|/remove|すべてのユーザーごとの監査ポリシー設定を削除し、すべてのシステム監査ポリシー設定を無効にします。</br>構文とオプションについては、 [Auditpol の削除](auditpol-remove.md)を参照してください。|
|/resourcesacl|グローバルリソースシステムアクセス制御リスト (Sacl) を構成します。</br>メモ:Windows 7 および Windows Server 2008 R2 にのみ適用されます。</br>[Auditpol resourceSACL](auditpol-resourcesacl.md)を参照してください。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

監査ポリシーのコマンドラインツールを使用すると、次のことができます。
-   システム監査ポリシーを設定し、クエリを実行します。
-   ユーザーごとの監査ポリシーを設定し、クエリを実行します。
-   監査オプションを設定および照会します。
-   監査ポリシーへのアクセスを委任するために使用されるセキュリティ記述子を設定および照会します。
-   監査ポリシーをレポートするか、コンマ区切り値 (CSV) テキストファイルにバックアップします。
-   CSV テキストファイルから監査ポリシーを読み込みます。
-   グローバルリソース Sacl を構成します。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)