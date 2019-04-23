---
title: wbadmin start systemstaterecovery
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 208b1be9-3452-4aba-bb49-46bc587fca96
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c99a934987e320baaec0e56c69f36eda5a32819
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852683"
---
# <a name="wbadmin-start-systemstaterecovery"></a>wbadmin start systemstaterecovery



場所と指定したバックアップからシステム状態の回復を実行します。

> [!NOTE]
> Windows Server バックアップはバックアップまたはシステム状態のバックアップまたはシステム状態の回復の一部としてユーザーのレジストリ ハイブ (HKEY_CURRENT_USER) を回復します。

このサブコマンドでシステム状態の回復を実行するには、メンバーである、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**、 をクリックし、**管理者として実行**)。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

Windows Server 2008 の構文:
```
wbadmin start systemstaterecovery
-version:<VersionIdentifier>
-showsummary
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:<TargetPathForRecovery>]
[-authsysvol]
[-quiet]
```
Windows Server 2008 R2 またはそれ以降の構文:
```
wbadmin start systemstaterecovery
-version:<VersionIdentifier>
-showsummary
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:<TargetPathForRecovery>]
[-authsysvol]
[-autoReboot]
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|バージョン|年/月/日に回復するバックアップのバージョン識別子を指定します-HH:MM の形式。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。|
|-showsummary|(操作を完了するために必要な再起動) 後に、最後のシステム状態の回復の概要を報告します。 その他のパラメーターはこのパラメーターを含めることはできません。|
|-backuptarget|バックアップまたは復元するバックアップを格納している記憶域の場所を指定します。 このパラメーターは、記憶域の場所は、このコンピューターのバックアップが通常格納場所と異なる場合に便利です。|
|-コンピューター|回復するコンピューターの名前を指定します。 このパラメーターは、複数のコンピューターを同じ場所にバックアップされている場合に便利です。 ときに使用する必要があります、 **-backuptarget** パラメーターを指定します。|
|-recoveryTarget|復元するディレクトリを指定します。 このパラメーターは、バックアップが別の場所に復元される場合に便利です。|
|-authsysvol|使用する場合は (システム ボリュームの共有ディレクトリ) の SYSVOL の authoritative restore を実行します。|
|-autoReboot|システム状態の回復操作の終了時にシステムを再起動することを指定します。 このパラメーターは、元の場所への回復のみ有効です。 回復操作の後の手順を実行する必要がある場合、このパラメーターを使用するはお勧めできません。|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|

## <a name="BKMK_examples"></a>例

-   午前 9時 00分を 03/31/2013 からシステム状態のバックアップの回復を実行するには、次のように入力します。  
    ```
    wbadmin start systemstaterecovery -version:03/31/2013-09:00
    ```  
-   午前 9時 00分 04/30/2013 からシステム状態のバックアップの回復を実行するには 共有リソース上に格納される\\ \\servername\share server01、種類。  
    ```
    wbadmin start systemstaterecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
    ```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [開始 WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx)コマンドレット