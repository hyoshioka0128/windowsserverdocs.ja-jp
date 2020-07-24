---
title: wbadmin start recovery
description: 指定したパラメーターに基づいて回復操作を実行する wbadmin start recovery のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 684e768979f54b772bffcb997b6ad44291dde8af
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954574"
---
# <a name="wbadmin-start-recovery"></a>wbadmin start recovery

指定したパラメーターに基づいて回復操作を実行します。

このサブコマンドを使用して回復を実行するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権のコマンドプロンプトを開くには、[**スタート**] ボタンをクリックし、[**コマンドプロンプト**] を右クリックして、[**管理者として実行**] をクリックします)。

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

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-version|復元するバックアップのバージョン識別子を MM/DD/YYYY-HH: MM 形式で指定します。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。|
|-項目|回復するボリューム、アプリケーション、ファイル、またはフォルダーのコンマ区切りの一覧を指定します。</br>- **Itemtype**が**volume**の場合、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を指定することによって、ボリュームを1つだけ指定できます。</br>- **Itemtype**が**App**の場合、1つのアプリケーションのみを指定できます。 回復するには、アプリケーションが Windows Server バックアップに登録されている必要があります。 また **、値の**表示方法を使用して、Active Directory のインストールを回復することもできます。 詳細については、「」の「解説」を参照してください。</br>- **Itemtype**が**File**の場合は、ファイルまたはフォルダーを指定できますが、同じボリュームの一部である必要があり、同じ親フォルダーの下にある必要があります。|
|-itemtype|回復する項目の種類を指定します。 **ボリューム**、**アプリ**、または**ファイル**である必要があります。|
|-backuptarget|回復するバックアップが格納されている記憶域の場所を指定します。 このパラメーターは、このコンピューターのバックアップが通常格納されている場所とは異なる場所にある場合に便利です。|
|-コンピューター|バックアップの回復先となるコンピューターの名前を指定します。 このパラメーターは、複数のコンピューターが同じ場所にバックアップされている場合に便利です。 **-BackupTarget**パラメーターが指定されている場合に使用する必要があります。|
|-recoveryTarget|復元先の場所を指定します。 このパラメーターは、この場所が以前にバックアップされた場所と異なる場合に便利です。 また、ボリューム、ファイル、またはアプリケーションの復元に使用することもできます。 ボリュームを復元する場合は、代替ボリュームのボリュームドライブ文字を指定できます。 ファイルまたはアプリケーションを復元する場合は、別の回復場所を指定できます。|
|-recursive|ファイルを回復する場合にのみ有効です。 フォルダー内のファイルと、指定したフォルダーの下位にあるすべてのファイルを回復します。 既定では、指定されたフォルダーに直接存在するファイルのみが回復されます。|
|-上書き|ファイルを回復する場合にのみ有効です。 回復中のファイルが同じ場所に既に存在する場合に実行する操作を指定します。</br>-   [**スキップ**] を Windows Server バックアップして、既存のファイルをスキップし、次のファイルの回復を続行します。</br>-   **"Createcopy"** は、既存のファイルが変更されないように、既存のファイルのコピーを作成する Windows Server バックアップします。</br>-   **上書き**を使用すると、Windows Server バックアップによって、バックアップからのファイルで既存のファイルが上書きされます。|
|-notRestoreAcl|ファイルを回復する場合にのみ有効です。 バックアップから回復するファイルのセキュリティアクセス制御リスト (Acl) を復元しないように指定します。 既定では、セキュリティ Acl が復元されます (既定値は**true です)**。 このパラメーターを使用すると、復元されたファイルの Acl は、ファイルの復元先の場所から継承されます。|
|-skipBadClusterCheck|ボリュームを回復する場合にのみ有効です。 無効なクラスター情報について、回復しているディスクのチェックをスキップします。 別のサーバーまたはハードウェアに回復する場合は、このパラメーターを使用しないことをお勧めします。 これらのディスクに対して**chkdsk/b**コマンドをいつでも手動で実行して、不良クラスターがないかどうかを確認し、それに応じてファイルシステム情報を更新することができます。</br>重要: 説明に従って**chkdsk**を実行するまでは、回復したシステムで報告された不良クラスターが正確でない可能性があります。|
|-noRollForward|アプリケーションを回復する場合にのみ有効です。 バックアップからの最新バージョンが選択されている場合に、アプリケーションの以前の特定の時点への復旧を許可します。 最新ではないその他のバージョンのアプリケーションでは、以前の特定の時点への復旧が既定値として行われます。|
|-quiet|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="remarks"></a>注釈

-   特定のバックアップバージョンから回復可能な項目の一覧を表示するには、 **wbadmin get items**を使用します。 バックアップ時にボリュームにマウントポイントまたはドライブ文字がない場合、このサブコマンドは、ボリュームの回復に使用する GUID ベースのボリューム名を返します。
-   **-Itemtype**が**App**の場合は、値を使用して、[メディア**からのインストール**]**操作を実行し、** Active Directory Domain Services に必要なすべての関連データを回復することができます。 次に、Active Directory データベース、レジストリ、および SYSVOL の状態のコピー**を作成し**、この情報を **-recoverytarget**で指定した場所に保存します。 このパラメーターは **、-recoverytarget**が指定されている場合にのみ使用してください。

>     [!NOTE]
>     Before using **wbadmin** to perform an install from media operation, you should consider using the **ntdsutil** command because **ntdsutil** only copies the minimum amount of data needed, and it uses a more secure data transport method.

## <a name="examples"></a>例

2013年3月31日の午前9:00 に撮影されたバックアップの回復を実行するには、次のように入力します。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
2013年3月31日のバックアップを実行するには、レジストリの午前9:00 に、次のように入力します。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
9:00 2013 年3月31日から、d:\folder の下位にある d:\folder とフォルダーのバックアップの回復を実行するには、次のように入力します。
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
9:00 2013 年3月31日からのバックアップの回復を実行するには、volume \\ \\ ? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963} \, type:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
2013年4月30日からのバックアップの回復を実行するには、server01 の共有フォルダー servername\share の午前9:00 に、 \\ \\ 次のように入力します。
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>その他のリファレンス

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBFileRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps)コマンドレット
-   [WBHyperVRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps)コマンドレット
-   [WBSystemStateRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps)コマンドレット
-   [WBVolumeRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps)コマンドレット
