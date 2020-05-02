---
title: wbadmin
description: コマンドプロンプトからオペレーティングシステム、ボリューム、ファイル、フォルダー、およびアプリケーションをバックアップして復元できる wbadmin のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94f07d17d46dad4e5301ba3ea6be94b10f26a3af
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725834"
---
# <a name="wbadmin"></a>wbadmin



では、コマンドプロンプトからオペレーティングシステム、ボリューム、ファイル、フォルダー、およびアプリケーションをバックアップおよび復元できます。

定期的にスケジュールされたバックアップを構成するには、 **Administrators**グループのメンバーである必要があります。 このコマンドを使用して他のすべてのタスクを実行する、 **Backup Operators** または **管理者** グループ、またはをされている必要が適切なアクセス許可を委任します。

実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権のコマンドプロンプトを開くには、[**コマンドプロンプト**] を右クリックし、[**管理者として実行**] をクリックします)。

## <a name="subcommands"></a>サブコマンド

|サブコマンド|[説明]|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|定期的にスケジュールされたバックアップを構成して有効にします。|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|毎日のバックアップを無効にします。|
|[Wbadmin start backup](wbadmin-start-backup.md)|1回限りのバックアップを実行します。 パラメーターを使用しない場合は、毎日のバックアップスケジュールの設定が使用されます。|
|[Wbadmin stop job](wbadmin-stop-job.md)|現在実行中のバックアップまたは回復操作を停止します。|
|[Wbadmin get versions](wbadmin-get-versions.md)|ローカルコンピューターから回復可能なバックアップの詳細を一覧表示するか、別の場所が指定されている場合は、別のコンピューターから復元します。|
|[Wbadmin get items](wbadmin-get-items.md)|バックアップに含まれる項目を一覧表示します。|
|[Wbadmin start recovery](wbadmin-start-recovery.md)|指定されたボリューム、アプリケーション、ファイル、またはフォルダーの回復を実行します。|
|[Wbadmin get status](wbadmin-get-status.md)|現在実行中のバックアップまたは回復操作の状態が表示されます。|
|[Wbadmin get disks](wbadmin-get-disks.md)|現在オンラインになっているディスクを一覧表示します。|
|[Wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|システム状態の回復を実行します。|
|[Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|システム状態のバックアップを実行します。|
|[Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|1つまたは複数のシステム状態のバックアップを削除します。|
|[Wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|(少なくともすべてのボリュームをオペレーティング システムの状態を含む) 完全なシステムの回復を実行します。 このサブコマンドは、Windows 回復環境を使用している場合にのみ使用できます。|
|[Wbadmin restore catalog](wbadmin-restore-catalog.md)|ローカルコンピューター上のバックアップカタログが破損している場合に、指定した記憶域の場所からバックアップカタログを回復します。|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|ローカル コンピューター上のバックアップ カタログを削除します。 このサブコマンドは、このコンピューター上のバックアップカタログが破損していて、カタログの復元に使用できる別の場所にバックアップが保存されていない場合にのみ使用してください。|

## <a name="additional-references"></a>その他のリファレンス

-   [バックアップと回復](https://go.microsoft.com/fwlink/?LinkID=195054)
-   [Windows PowerShell の Windows Server バックアップコマンドレット](https://technet.microsoft.com/library/jj902428.aspx)