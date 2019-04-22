---
title: wbadmin delete systemstatebackup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 707d37cb-448d-4542-b6ac-1fc89e749788
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6801ca5985af626ccb7f6170fbcd6f8fc8305ba1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813153"
---
# <a name="wbadmin-delete-systemstatebackup"></a>wbadmin delete systemstatebackup



指定したシステム状態のバックアップを削除します。 指定したボリュームがローカル サーバーのシステム状態バックアップ以外のバックアップを含んでいる場合、それらのバックアップは削除されません。

> [!NOTE]
> Windows Server バックアップはバックアップまたはシステム状態のバックアップまたはシステム状態の回復の一部としてユーザーのレジストリ ハイブ (HKEY_CURRENT_USER) を回復します。

このサブコマンドでシステム状態のバックアップを削除するには、メンバーである、 **Backup Operators** グループ、または **管理者** グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**、 をクリックし、**管理者として実行**)。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
wbadmin delete systemstatebackup
{-keepVersions:<NumberofCopies> | -version:<VersionIdentifier> | -deleteOldest}
[-backupTarget:<VolumeName>]
[-machine:<BackupMachineName>]
[-quiet]
```

> [!IMPORTANT]
> これらのパラメーターの 1 つだけを指定する必要があります: **- keepVersions**, 、**-バージョン**, 、または **- deleteOldest**します。

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-keepVersions|最新のシステム状態バックアップを保持する数を指定します。 値は正の整数である必要があります。 パラメーター値 **- keepVersions: 0** すべてのシステム状態のバックアップを削除します。|
|バージョン|年/月/日で、バックアップのバージョン識別子を指定します-HH:MM の形式です。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。</br>システム状態のバックアップのみのバージョンを削除するには、このコマンドを使用します。 使用 **wbadmin 項目を取得する** のバージョンの種類を表示します。|
|-deleteOldest|最も古いシステム状態のバックアップを削除します。|
|-backuptarget|削除するバックアップ用ストレージの場所を指定します。 ディスクのバックアップ用ストレージの場所には、ドライブ文字、マウント ポイント、または GUID ベースのボリュームのパスを指定できます。 この値は、ローカル コンピューターではなくバックアップを検索するために指定するだけです。 ローカル コンピューターのバックアップの詳細については、ローカル コンピューター上のバックアップ カタログで利用可能なになります。|
|-コンピューター|コンピューターを削除するがシステム状態のバックアップを指定します。 複数のコンピューターが同じ場所にバックアップされた場合に役立ちます。 ときに使用する必要があります、 **-backuptarget** パラメーターを指定します。|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|

## <a name="BKMK_examples"></a>例

2013 年 3 月 31 日の午前 10時 00分時に作成、システム状態バックアップを削除するには、次のように入力します。
```
wbadmin delete systemstatebackup -version:03/31/2013-10:00
```
最新の 3 つを除く、すべてのシステム状態バックアップを削除するには、次のように入力します。
```
wbadmin delete systemstatebackup -keepVersions:3
```
ディスク f に保存されている最も古いシステム状態のバックアップを削除するには、次のように入力します。
```
wbadmin delete systemstatebackup -backupTarget:f -deleteOldest
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)