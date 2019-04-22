---
title: wbadmin start recovery
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f24c9dfeb0ce87474e58d3bd2bce8b68e31cb63
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823283"
---
# <a name="wbadmin-start-recovery"></a>wbadmin start recovery



指定したパラメーターに基づいて、復旧操作を実行します。

このサブコマンドで回復を実行する、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (コマンド プロンプトを開くにはクリックして **開始**, を右クリックして **コマンド プロンプト**, 、クリックして **管理者として実行**.)

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
wbadmin start recovery
-version:<VersionIdentifier>
-items:{<VolumesToRecover> | <AppsToRecover> | <FilesOrFoldersToRecover>}
-itemtype:{Volume | App | File}
[-backupTarget:{<VolumeHostingBackup> | <NetworkShareHostingBackup>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:{<TargetVolumeForRecovery> | <TargetPathForRecovery>}]
[-recursive]
[-overwrite:{Overwrite | CreateCopy | Skip}]
[-notRestoreAcl]
[-skipBadClusterCheck]
[-noRollForward]
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|バージョン|年/月/日に回復するバックアップのバージョン識別子を指定します-HH:MM の形式。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。|
|-項目|回復するボリューム、アプリケーション、ファイル、またはフォルダーのコンマ区切りの一覧を指定します。</br>If **- itemtype**は**ボリューム**、1 つのボリュームだけを指定することができます、ボリュームのドライブ文字、ボリュームのマウント ポイント、または GUID ベースのボリューム名を提供することで。</br>If **- itemtype**は**アプリ**、1 つのアプリケーションのみを指定することができます。 回復するには、Windows Server バックアップでアプリケーションを登録が必要があります。 値を使用することもできます。 **ADIFM** Active Directory のインストールを回復します。 詳細については、「解説」を参照してください。</br>If **- itemtype**は**ファイル**、ファイルまたはフォルダーを指定することができますが、同じボリュームの一部である必要があり、同じ親フォルダーがあります。|
|-itemtype|回復する項目の種類を指定します。 必要があります**ボリューム**、**アプリ**、または**ファイル**します。|
|-backuptarget|回復するバックアップを保持するストレージの場所を指定します。 このパラメーターは、場所はこのコンピューターのバックアップが通常格納場所と異なる場合に便利です。|
|-コンピューター|バックアップを回復するコンピューターの名前を指定します。 このパラメーターは、複数のコンピューターを同じ場所にバックアップされている場合に便利です。 必要がある場合に使用、 **-backuptarget**パラメーターを指定します。|
|-recoveryTarget|復元する場所を指定します。 このパラメーターは、この場所は既にバックアップされている場所と異なる場合に便利です。 これは、ボリューム、ファイル、またはアプリケーションの復元の場合も使用できます。 ボリュームを復元する場合は、別のボリュームのボリュームのドライブ文字を指定できます。 ファイルまたはアプリケーションを復元する場合は、代替回復の場所を指定できます。|
|-再帰|ファイルを回復する場合にのみ有効です。 フォルダー内のファイルと、指定したフォルダーの下位のすべてのファイルを回復します。 既定では、直接、指定したフォルダー内にあるファイルのみが復旧されます。|
|-上書き|ファイルを回復する場合にのみ有効です。 同じ場所にまだ復旧されているファイルが存在する場合に実行するアクションを指定します。</br>-   **Skip**と Windows Server のバックアップを既存のファイルをスキップし、次のファイルの回復を続行します。</br>-   **CreateCopy**により、既存のファイルが修正されないように、既存のファイルのコピーを作成する Windows Server バックアップします。</br>-   **上書き**と Windows Server バックアップ、バックアップからファイルを使用して、既存のファイルを上書きします。|
|-notRestoreAcl|ファイルを回復する場合にのみ有効です。 バックアップから回復するファイルのセキュリティのアクセス制御リスト (Acl) のない復元を指定します。 既定では、セキュリティ Acl が復元されます (既定値は**true)** します。 このパラメーターを使用する場合、復元されたファイルの Acl は、ファイルの復元先の場所から継承されます。|
|-skipBadClusterCheck|ボリュームを回復する場合にのみ有効です。 不良クラスターについては、回復ディスクのチェックをスキップします。 別のサーバーまたはハードウェアに回復する場合は、このパラメーターを使用しないことをお勧めします。 コマンドを手動で実行することができます**chkdsk/b**不良クラスターは、それらを確認し、ファイル システムの情報を適宜更新するには、いつでもこれらのディスク。</br>重要:実行するまで**chkdsk**ように、回復したシステムに報告された不良クラスターは正確なできない可能性があります。|
|-noRollForward|アプリケーションを回復する場合にのみ有効です。 バックアップからの最新バージョンが選択されている場合、アプリケーションの前の時点に回復できます。 アプリケーションの他のバージョン、前の最新の時点の回復は、既定値として行われます。|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|

## <a name="remarks"></a>注釈

-   特定のバックアップ バージョンからの回復可能なアイテムの一覧を表示する使用**wbadmin get 項目**します。 ボリュームのバックアップ時にマウント ポイントまたはドライブ文字のない場合、このサブコマンドは、ボリュームの回復に使用する必要があります GUID ベースのボリューム名を返します。
-   ときに、 **- itemtype**は**アプリ**の値を使用する**ADIFM**の **-項目**すべてを回復する操作をメディアからインストールを実行する、Active Directory Domain Services に必要な関連データ。 **ADIFM** Active Directory データベース、レジストリ、および SYSVOL の状態のコピーを作成しで指定された場所でこの情報を保存 **-recoverytarget**します。 このパラメーターを使用する場合にのみ **-recoverytarget**を指定します。

>     [!NOTE]
>     Before using **wbadmin** to perform an install from media operation, you should consider using the **ntdsutil** command because **ntdsutil** only copies the minimum amount of data needed, and it uses a more secure data transport method.

## <a name="BKMK_Examples"></a>例

2013 年 3 月 31日、午前 9時 00分、ボリューム d: の取得から、バックアップの回復を実行するには、次のように入力します。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
2013 年 3 月 31日、午前 9時 00分、レジストリの作成から、回復を実行してドライブ d のバックアップの次のように入力します。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
2013 年 3 月 31日、午前 9時 00分、d:\folder との下位に d:\folder、フォルダーの取得から、バックアップの回復を実行するには、次のように入力します。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
午前 9時 00分、ボリュームの作成時刻、2013 年 3 月 31 日から、バックアップの回復を実行する\\ \\? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\,型。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume 
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
午前 9時 00分、共有フォルダーの取得、2013 年 4 月 30 日から、バックアップの回復を実行する\\ \\servername\share server01、タイプから。
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [開始 WBFileRecovery](https://technet.microsoft.com/library/jj902457.aspx)コマンドレット
-   [開始 WBHyperVRecovery](https://technet.microsoft.com/library/jj902463.aspx)コマンドレット
-   [開始 WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx)コマンドレット
-   [開始 WBVolumeRecovery](https://technet.microsoft.com/library/jj902470.aspx)コマンドレット