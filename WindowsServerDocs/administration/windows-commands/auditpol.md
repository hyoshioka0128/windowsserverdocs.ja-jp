---
title: auditpol
description: Windows コマンド」のトピック**auditpol** - に関する情報を表示し、監査ポリシーを操作する関数を実行します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d7e8364be977e868ac161704e67c37ec5c400e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849223"
---
# <a name="auditpol"></a>auditpol



に関する情報を表示し、監査ポリシーを操作する関数を実行します。

このコマンドの使用方法の例については、各トピックの「例」セクションを参照してください。

## <a name="syntax"></a>構文

```
Auditpol command [<sub-command><options>]
```

## <a name="parameters"></a>パラメーター

|サブ コマンド|説明|
|-----------|-----------|
|/get|現在の監査ポリシーが表示されます。</br>参照してください[Auditpol get](auditpol-get.md)構文とオプションについてです。|
|/set|監査ポリシーを設定します。</br>参照してください[Auditpol 設定](auditpol-set.md)構文とオプションについてです。|
|/list|選択可能なポリシーの要素が表示されます。</br>参照してください[Auditpol 一覧](auditpol-list.md)構文とオプションについてです。|
|/backup|監査ポリシーをファイルに保存します。</br>参照してください[Auditpol バックアップ](auditpol-backup.md)構文とオプションについてです。|
|/restore|Auditpol/backup を使用して作成されたファイルから、監査ポリシーを復元します。</br>参照してください[Auditpol 復元](auditpol-restore.md)構文とオプションについてです。|
|/clear|監査ポリシーを消去します。</br>参照してください[Auditpol オフ](auditpol-clear.md)構文とオプションについてです。|
|/remove|すべてのユーザーごとの監査ポリシーの設定を削除し、すべてのシステム監査ポリシー設定を無効にします。</br>参照してください[Auditpol 削除](auditpol-remove.md)構文とオプションについてです。|
|/resourceSACL|グローバル リソース システム アクセス制御リスト (Sacl) を構成します。</br>注:7 および Windows Server 2008 R2、Windows にのみ適用されます。</br>参照してください[Auditpol resourceSACL](auditpol-resourcesacl.md)します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

監査ポリシーのコマンド ライン ツールを使用できます。
-   設定して、システム監査ポリシーをクエリします。
-   設定して、ユーザーごとの監査ポリシーをクエリします。
-   設定して、監査オプションをクエリします。
-   設定して、監査ポリシーへのアクセスを委任するために使用するセキュリティ記述子をクエリします。
-   レポートまたはコンマ区切り値 (CSV) テキスト ファイルに、監査ポリシーをバックアップします。
-   監査ポリシーは、CSV テキスト ファイルから読み込みます。
-   グローバル リソース Sacl を構成します。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)