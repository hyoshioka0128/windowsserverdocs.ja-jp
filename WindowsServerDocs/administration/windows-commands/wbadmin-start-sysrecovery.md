---
title: wbadmin start sysrecovery
description: Wbadmin start sysrecovery のリファレンストピックでは、指定したパラメーターを使用してシステム回復 (ベアメタル回復) を実行します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba3d826b0312091f00ef01d2efe9ee63572fade1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725892"
---
# <a name="wbadmin-start-sysrecovery"></a>wbadmin start sysrecovery



指定されたパラメーターを使用して、システム回復 (ベアメタル回復) を実行します。

> [!NOTE]
> このサブコマンドは、Windows 回復環境からのみ実行でき、 **Wbadmin**の使用法テキストには既定では表示されません。 詳細については、「 [Windows 回復環境 (WINDOWS RE) の概要](https://technet.microsoft.com/library/hh825173.aspx)」を参照してください。

このサブコマンドを使用してシステムの回復を実行するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。

## <a name="syntax"></a>構文

```
wbadmin start sysrecovery
-version:<VersionIdentifier>
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-restoreAllVolumes]
[-recreateDisks]
[-excludeDisks]
[-skipBadClusterCheck]
[-quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|-version|復元するバックアップのバージョン識別子を MM/DD/YYYY-HH: MM 形式で指定します。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。|
|-backuptarget|回復する 1 つ以上のバックアップが格納されている記憶域の場所を指定します。 このパラメーターは、このコンピューターのバックアップが通常格納されている場所とは異なる場所に保存されている場合に便利です。|
|-コンピューター|回復するコンピューターの名前を指定します。 このパラメーターは、複数のコンピューターが同じ場所にバックアップされている場合に便利です。 ときに使用する必要があります、 **-backuptarget** パラメーターを指定します。|
|-restoreAllVolumes|選択したバックアップからすべてのボリュームを回復します。 このパラメーターが指定されていない場合、重要なボリューム (システム状態およびオペレーティングシステムコンポーネントを含むボリューム) のみが回復されます。 このパラメーターは、システムの回復中に重要ではないボリュームを回復する必要がある場合に便利です。|
|-recreateDisks|バックアップの作成時に存在していた状態にディスク構成を回復します。</br>警告: このパラメーターは、オペレーティングシステムコンポーネントをホストするボリューム上のすべてのデータを削除します。 データボリュームからデータを削除することもできます。|
|-excludeDisks|**-Recreatedisks**パラメーターと共に指定する場合にのみ有効です。 **wbadmin get disks**の出力に示されているように、ディスク識別子のコンマ区切りリストとして入力する必要があります。 除外されたディスクはパーティション分割またはフォーマットされていません。 このパラメーターは、復旧操作中に変更したくないディスク上のデータを保持するのに役立ちます。|
|-skipBadClusterCheck|回復ディスクの不適切なクラスター情報の確認をスキップします。 別のサーバーまたはハードウェアに復元する場合は、このパラメーターを使用しないことをお勧めします。 回復ディスクで**chkdsk/b**をいつでも手動で実行して、不良クラスターを確認し、それに応じてファイルシステム情報を更新することができます。</br>警告: 説明に従って**chkdsk**を実行するまで、回復したシステムで報告された不良クラスターが正確でない可能性があります。|
|-quiet|ユーザーにプロンプトを表示せずにコマンドを実行します。|

## <a name="examples"></a>例

2013年3月31日に9:00 午前5時に実行されたバックアップからの情報の回復を開始するには、次のように入力します。
```
wbadmin start sysrecovery -version:03/31/2013-09:00 -backupTarget:d:
```
9:00 2013 年4月30日に実行されたバックアップからの情報の回復を開始するには、共有\\ \\フォルダー servername\shared: server01 に、次のように入力します。
```
wbadmin start sysrecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBBareMetalRecovery](https://technet.microsoft.com/library/jj902461.aspx)コマンドレット