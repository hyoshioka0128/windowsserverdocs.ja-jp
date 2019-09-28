---
title: wbadmin start systemstaterecovery
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6ae534eed26629be264b698869edc57232e2b571
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362225"
---
# <a name="wbadmin-start-systemstaterecovery"></a>wbadmin start systemstaterecovery



指定したバックアップから、場所とシステム状態の回復を実行します。

> [!NOTE]
> Windows Server バックアップはバックアップまたはシステム状態のバックアップまたはシステム状態の回復の一部としてユーザーのレジストリ ハイブ (HKEY_CURRENT_USER) を回復します。

このサブコマンドを使用してシステム状態の回復を実行するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

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
Windows Server 2008 R2 以降の構文:
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
|バージョン|復元するバックアップのバージョン識別子を MM/DD/YYYY-HH: MM 形式で指定します。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。|
|-showsummary|最後のシステム状態の回復の概要を報告します (操作を完了するために再起動が必要になった後)。 このパラメーターを他のパラメーターと共に指定することはできません。|
|-backuptarget|回復するバックアップが格納されている記憶域の場所を指定します。 このパラメーターは、記憶域の場所が、このコンピューターのバックアップが通常格納されている場所と異なる場合に便利です。|
|-コンピューター|回復するコンピューターの名前を指定します。 このパラメーターは、複数のコンピューターが同じ場所にバックアップされている場合に便利です。 ときに使用する必要があります、 **-backuptarget** パラメーターを指定します。|
|-recoveryTarget|復元先のディレクトリを指定します。 このパラメーターは、バックアップを別の場所に復元する場合に便利です。|
|-authsysvol|使用すると、SYSVOL (システムボリュームの共有ディレクトリ) の authoritative restore が実行されます。|
|-autoReboot|システム状態の回復操作の最後にシステムを再起動することを指定します。 このパラメーターは、元の場所への回復に対してのみ有効です。 回復操作の後で手順を実行する必要がある場合は、このパラメーターを使用しないことをお勧めします。|
|-通知の停止|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="BKMK_examples"></a>例

- 03/31/2013 の午前9:00 にバックアップのシステム状態の回復を実行するには、次のように入力します。  
  ```
  wbadmin start systemstaterecovery -version:03/31/2013-09:00
  ```  
- 04/30/2013 の午前9:00 にバックアップのシステム状態の回復を実行するには 共有リソースに格納されている \\ @ no__t-1servername\share for server01, 次のように入力します。  
  ```
  wbadmin start systemstaterecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
  ```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx)コマンドレット