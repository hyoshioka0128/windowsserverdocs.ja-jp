---
title: wbadmin get 項目
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27d08ce3-6e06-4260-b264-fc1bde132d09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eeb7c29ff552f968b4785612f626a86baf154ad7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842883"
---
# <a name="wbadmin-get-items"></a>wbadmin get 項目



特定のバックアップに含まれるアイテムを一覧表示します。

このサブコマンドを使用する、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**し**管理者として実行**)。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
wbadmin get items
-version:<VersionIdentifier>
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|バージョン|年/月/日で、バックアップのバージョンを指定します。-HH:MM の形式。 バージョン情報がわからない場合は、入力**wbadmin のバージョンを取得する**します。|
|-backuptarget|詳細情報の対象となるバックアップを格納しているストレージの場所を指定します。 そのターゲットの場所に格納されているバックアップを一覧表示するために使用します。 バックアップ ターゲットの場所には、ローカルに接続されたディスク ドライブまたはリモート共有フォルダーを指定できます。 場合**wbadmin get 項目**実行は、バックアップが作成された、同じコンピューターでこのパラメーターは必要ありません。 ただし、このパラメーターは、別のコンピューターから作成されたバックアップに関する情報の取得に必須です。|
|-コンピューター|バックアップの詳細を使用するコンピューターの名前を指定します。 複数のコンピューターを同じ場所にバックアップされている場合に役立ちます。 ときに使用する必要があります **-backuptarget**を指定します。|

## <a name="BKMK_examples"></a>例

項目を一覧表示、2013 年 3 月 31 日の午前 9 時まで、型に実行されたバックアップから。
```
wbadmin get items -version:03/31/2013-09:00
```
2013 年 4 月 30 日の午前 9 時に実行された server01 のバックアップからのリスト項目に 格納されていると\\ \\servername\share、種類。
```
wbadmin get items -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get WBBackupSet](https://technet.microsoft.com/library/jj902473.aspx)コマンドレット