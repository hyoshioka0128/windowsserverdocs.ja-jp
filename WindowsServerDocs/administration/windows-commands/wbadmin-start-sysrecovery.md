---
title: wbadmin start sysrecovery
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8e0ff114d09d70b9e50e8c4ea6af6330c74128c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847163"
---
# <a name="wbadmin-start-sysrecovery"></a>wbadmin start sysrecovery



指定したパラメーターを使用して、システム回復 (ベア メタル回復) を実行します。

> [!NOTE]
> このサブコマンドは、Windows 回復環境からのみ実行できるし、既定の使用状況のテキストで表示されていない**Wbadmin**します。 詳細については、次を参照してください。 [Windows 回復環境 (Windows RE) の概要](https://technet.microsoft.com/library/hh825173.aspx)します。

このサブコマンドでシステム回復を実行する、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

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

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|バージョン|年/月/日に回復するバックアップのバージョン識別子を指定します-HH:MM の形式。 バージョン識別子を把握していない場合は、入力 **wbadmin のバージョンを取得する**です。|
|-backuptarget|バックアップまたは復元するバックアップを格納している記憶域の場所を指定します。 このパラメーターは、記憶域の場所は、このコンピューターのバックアップが通常格納場所と異なる場合に便利です。|
|-コンピューター|回復するコンピューターの名前を指定します。 このパラメーターは、複数のコンピューターを同じ場所にバックアップされている場合に便利です。 ときに使用する必要があります、 **-backuptarget** パラメーターを指定します。|
|-restoreAllVolumes|選択したバックアップからすべてのボリュームを回復します。 このパラメーターが指定されていない場合のみ重要なボリューム (システム状態とオペレーティング システムのコンポーネントが含まれているボリューム) が復旧されます。 このパラメーターは、システムの回復中に致命的でないボリュームを回復する必要がある場合に便利です。|
|-recreateDisks|バックアップの作成時に存在していた状態のディスク構成を復元します。</br>警告:このパラメーターは、そのコンポーネントをホスト オペレーティング システム ボリューム上のすべてのデータを削除します。 データ ボリュームからデータを削除、可能性があります。|
|-excludeDisks|指定した場合にのみ有効、 **- recreateDisks**パラメーターおよびディスク識別子のコンマ区切りのリストとして入力する必要があります (の出力に記載されている**wbadmin get ディスク**)。 除外されたディスクのパーティション分割または書式設定はできません。 このパラメーターは、回復操作中に変更したくないディスク上のデータを保持するのに役立ちます。|
|-skipBadClusterCheck|不良クラスターについては、回復ディスクの確認をスキップします。 別のサーバーまたはハードウェアに復元する場合は、このパラメーターを使用しないことをお勧めします。 手動で実行することができます**chkdsk/b**不良クラスターは、それらを確認し、ファイル システムの情報を適宜更新するには、いつでも、回復ディスクにします。</br>警告:実行するまで**chkdsk**ように、回復したシステムに報告された不良クラスターは正確なできない可能性があります。|
|-通知の停止|ユーザーにプロンプトを表示せずに、コマンドを実行します。|

## <a name="BKMK_examples"></a>例

情報を 2013 年 3 月 31 日の午前 9 時に実行されたバックアップから回復を開始するには、d: ドライブの種類にあります。
```
wbadmin start sysrecovery -version:03/31/2013-09:00 -backupTarget:d:
```
共有フォルダー内にある情報を 2013 年 4 月 30 日の午前 9 時に実行されたバックアップから回復を開始する\\ \\servername\shared: server01 を入力します。
```
wbadmin start sysrecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get WBBareMetalRecovery](https://technet.microsoft.com/library/jj902461.aspx)コマンドレット